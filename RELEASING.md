# Releasing the lesson and depositing the data on Zenodo

This note is for the maintainers. It explains how the GitHub and Zenodo sides fit together and lists every step in order. Readers do not need it.

## How the two sides fit together

There are two separate Zenodo records:

1. **The dataset record.** A manual upload of `cleaned_data_v3_pt.tar.gz` (about 2 GB). Zenodo hosts the file and mints a DOI. The lesson links to it. Nothing about it lives on GitHub except the link.
2. **The lesson record.** Created automatically by Zenodo's GitHub integration every time we publish a GitHub *release* of this repository. Zenodo stores a zip of the repository at that tag, mints a version DOI, and keeps one *concept* DOI that always points at the newest version. The metadata for this record (authors, ORCIDs, licence, keywords, link to the dataset) comes from the `.zenodo.json` file in this repository, so it stays correct without anyone retyping it.

Placeholders in the repository mark where the two DOI numbers go:

- `ZENODO-DATASET-DOI` marks the dataset's DOI number.
- `ZENODO-LESSON-DOI` marks the lesson's concept DOI number.

They appear in `README.md`, `part-2-analyzing-data.md`, `CITATION.cff` and `.zenodo.json`. A single find-and-replace (step 5 below) fills them all in.

## Step 1. Deposit the dataset and reserve its DOI

1. Download `cleaned_data_v3_pt.tar.gz` from Brian's Google Drive share (file id `1N3KSYepkSvgUil-518vOxcYU_80v2EEg`).
2. Record its MD5 checksum and size for the record description:

   ```
   md5 cleaned_data_v3_pt.tar.gz
   ls -l cleaned_data_v3_pt.tar.gz
   ```

3. Log in to https://zenodo.org (an ORCID login works) and choose **New upload**.
4. Upload the archive. Zenodo will show its own MD5 next to the file once uploaded; it should match yours.
5. Fill in the metadata:
   - Resource type: **Dataset**
   - Title: *PolyGraphs simulation output: trust, scepticism and mis-/disinformation on random, Barabási-Albert and Watts-Strogatz networks (cleaned_data_v3_pt)*, or similar
   - Creators, in this order, with ORCIDs and affiliation Northeastern University London: Brian Ball (0000-0003-2478-6151), David Freeborn (0000-0002-2117-8145), Federica Imbriale (0009-0009-2713-4547), Amil Mohanan (0000-0001-8408-7198). Nicolas Kuri is a lesson author but not a dataset author.
   - Description: what the simulations are (PolyGraphs, 100,000-step runs, 64 agents, the ops and network kinds covered), that the data are synthetic, how to unpack, and that the data accompany the lesson at the lesson's GitHub URL.
   - Licence: **Creative Commons Attribution 4.0 International**
   - Keywords: PolyGraphs, agent-based modelling, social epistemology, misinformation, network science
   - Related works: "is supplement to" the GitHub repository URL. Add the lesson DOI here later once it exists.
6. Under the DOI field choose **Get a DOI now** (Zenodo calls this reserving a DOI). Copy the number after `10.5281/zenodo.`. You can publish the record straight away or leave it as a draft until the lesson is released; the DOI does not change.

## Step 2. Create the GitHub repository

1. In the `nulcpl` organisation create a **public** repository named `polygraphs-lesson`.
2. Push the contents of this folder to its `main` branch.

## Step 3. Enable the Zenodo–GitHub integration

1. In Zenodo go to your account menu, then **GitHub**. Log in with the GitHub account that is an admin of `nulcpl` and authorise Zenodo.
2. Find `nulcpl/polygraphs-lesson` in the list and flip its switch to **On**. If the organisation's repositories are not listed, grant Zenodo access to the `nulcpl` organisation in GitHub under Settings, Applications, Authorized OAuth Apps, Zenodo.
3. Do nothing else here. Zenodo is now waiting for a release.

## Step 4. Publish the first release

1. On GitHub open **Releases**, then **Draft a new release**.
2. Tag `v1.0.0`, target `main`, title `v1.0.0`, and a one-line description. Publish it.
3. Within a few minutes the repository appears in Zenodo's GitHub page with a DOI badge. Open it and note the **concept DOI** (Zenodo shows it as "Cite all versions" on the record page). Copy the number after `10.5281/zenodo.`.

## Step 5. Fill in the DOIs and re-release

From the repository root, with the two numbers to hand:

```
DATASET=1234567   # number from step 1
LESSON=7654321    # concept DOI number from step 4
grep -rl "ZENODO-DATASET-DOI\|ZENODO-LESSON-DOI" . --exclude-dir=.git \
  | xargs sed -i '' -e "s/ZENODO-DATASET-DOI/$DATASET/g" -e "s/ZENODO-LESSON-DOI/$LESSON/g"
```

(On Linux use `sed -i` without the empty quotes.) Also uncomment the `doi:` line in `CITATION.cff`, set `date-released` to today, bump `version` to `1.0.1`, commit, and publish release `v1.0.1`. Zenodo archives the new version automatically; the concept DOI is unchanged and now resolves to a copy that carries both DOIs.

Finally, on the dataset record on Zenodo, edit the metadata to add the lesson's concept DOI under Related works ("is supplemented by"). This links the two records in both directions.

## Later changes

- Any edit to the lesson: commit to `main`, bump `version` and `date-released` in `CITATION.cff`, and publish a new release. Zenodo adds a new version under the same concept DOI.
- A new version of the dataset: on Zenodo open the dataset record and choose **New version**, upload the new file, publish. The old version keeps its DOI; update the link in `README.md` and `part-2-analyzing-data.md` only if you want readers to get the new version.
