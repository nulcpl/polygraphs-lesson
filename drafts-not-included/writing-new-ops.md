# Writing your own operation in four simple steps
This section is intended as a small (and surely not exhaustive) guide on how to write your own operation in Polygraphs. 

Before getting started, let's introduce some of Polygraphs vocabulary. Operations in Polygraphs are written as class objects. The simulation has several stages, but four of them are where most custom modifications happen: 1. **Data quality**: what kind of data agents observe (accurate or misleading?) 2. **Data collection**: who observes data 3. **Evidence sharing**: who communicates observed data with her neighbours 4. **Receivers' behavior**: do receivers fully trust the evidence? do they revisit their beliefs accordingly?

These stages correspond to 4 functions. You will want to modify each of these depending on the stage in which you wish to intervene:
1. Data quality -- **sample()**
2. Data collection -- **experiment()**
3. Evidence sharing -- **filterfn()**
4. Receivers' behavior -- **applyfn()**

With this in mind, we can get started on our new operation. For explanatory simplicity, we will here work on a small modification. For instance, in the standard BalaGoyalOp, **evidence sharing** among neighbours is always active -- whenever agents collect evidence, they share the results with their neighbours. But let's say we wanted to impose a stricter condition on evidence sharing: for example, making it so that only agents whose belief is > 0.7 share evidence. We would do this by overriding our filterfn(), the function that governs which nodes share evidence. 

You can write your own operation by adding it to the folder called 'ops' in your own copy of polygraphs. Let's write the operation together following these **4 steps**: 

1. Create your own file into 'ops', for instance: `new.py`
2. Open the file. At the top, import the parent class you want to inherit from:
`from .common import BalaGoyalOp`
3. Define your op as a subclass of the chosen parent class: `class NewOp(BalaGoyalOp):`
4. Choose the function(s) you want to override. This will obviously depend on what you want your new operation to do. In our case, we want to govern evidence sharing, so we  need to override filterfn(). The function governs which nodes share evidence by returning a 1-D boolean tensor, with one entry per edge: True = keep, False = drop. In **BalaGoyalOp** this is all the function contains: 
`return torch.gt(edges.src["payoffs"][:, 1], 0.0)` which returns True only for nodes that have generated evidence, so no empty messages get passed. All we need to do, then, is add a further condition. We can do this using `torch.gt(edges.src["beliefs"], 0.7)` which returns a tensor with value True for source nodes whose beliefs are greater than 0.7. We also want to keep the previous condition (discard nodes without evidence), so we will need to add it back, as it would just get overriden otherwise. 

We now have everything we need to write our operator: 

```python
"""
Confident sharer op: only nodes with belief > 0.7 share evidence.
"""

import torch

from .common import BalaGoyalOp


class ConfidentSharerOp(BalaGoyalOp):
    """
    Variant of Bala & Goyal where only confident nodes (belief > 0.7)
    share their evidence with neighbours.
    """

    def filterfn(self):
        """
        Keep edges only if the source node has belief > 0.7
        AND has evidence to share (trials > 0).
        """
        def function(edges):
            confident = torch.gt(edges.src["beliefs"], 0.7)
            has_evidence = torch.gt(edges.src["payoffs"][:, 1], 0.0)
            return confident & has_evidence
        return function
```
  You will notice we have also imported `torch` at the start of our file, as it is a library we use in our code. the return statement at the end of `function(edges)` returns a tensor with value True only for source nodes whose belief is higher than 0.7 AND (&) have evidence to pass on. Everything else stays as in our parent class `BalaGoyalOp`. 
  
  All done. We have just created a new operation!