# Current g3t Use Cases

## Evotypes User Journey

Generally, the process
1. Transfer CRAMs from the Cambridge on-prem to our OHSU buckets
2. Process a combination of files from Cambridge and ICGC sources...
   1. alignment to convert CRAMs -> BAMs (to stdize across all orgs doing processing)
   2. BAMs -> VCFs too?
3. Share processed files with collaborators (eg: chr1_allele_counts.txt)

### Cambridge Data Transfer Use Case

As an Evotypes collaborator, I want to transfer files from the Cambridge head node to OHSU buckets so that I can do processing on these files.

**Current State**
- Splitting up manifest created by `g3t push` to generate *n* manifests for each of the *n* files, running *n* `gen3-client upload-multiple` commands
- Manual tracking of files that have been transferred over (combo of spreadsheets and looking at the state of the bucket)

**Problems encountered**
*cannot do = bugfix of functionality; difficult to do = rework of docs/functionality + guardrails*
- [Cannot do] Unable to upload files in parallel using gen3
- [Cannot do] unable to push to production external (ACED-IDP)
- [difficult to do] Unable to add -> meta init -> push for the same project (push --overwrite adds all the files, so if push fails how to reupload just the one file)

**Improvements to Make**
- Resolve projects 
- resolve existing problems with upload to (waiting on exact error)
- - Spec out the use case for uploading files in parallel -> 