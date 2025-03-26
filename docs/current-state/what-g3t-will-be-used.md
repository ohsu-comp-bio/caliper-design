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

*cannot do* = no functionality exists in g3t, workarounds needed

*difficult to do* = rework of docs/functionality + guardrails

- [Cannot do] Unable to upload files in parallel using gen3
- [Cannot do] unable to push to production external (ACED-IDP)
- [difficult to do] Unable to add -> meta init -> push for the same project (push --overwrite adds all the files, so if push fails how to reupload just the one file)

See the below example workflow for uploading files to OHSU bucket (ACED production)
```sh
mkdir aced-evotypes_transfer
cd aced-evotypes_transfer
conda activate gen3_transfer

g3t init aced-evotypes_transfer

g3t add <FILE>
g3t add <FILE> 
g3t add <FILE>

# generate manifest file
g3t meta init
git add META && git commit -m "add META and cambridge files"
g3t push --overwrite

ctrl + c  #cancel once upload starts

# split manifest file into multiple json files (1 object per file)
cd .g3t/work

for i in $(seq $(jq '.|length' manifest-20250304205905.json)); do \
    j=$( expr $i - 1 ); \
    jq ".[$j]" manifest-20250304205905.json > $j.json;  \
done

# upload files via gen3-client (can upload multiple files at the same time)
tmux new -s mySession14
conda activate gen3_transfer
gen3-client upload-multiple --manifest /rds/project/rds-DNda7MnDzRs/evotypes/iq_transfer/aced-evotypes_transfer/.g3t/work/14.json --profile aced --upload-path /rds/project/rds-DNda7MnDzRs/evotypes/iq_transfer/aced-evotypes_transfer/ --bucket aced-ohsu-production --numparallel 75

#mySession24 LP6008340-DNA_E03.bam
tmux new -s mySession24
conda activate gen3_transfer
gen3-client upload-multiple --manifest /rds/project/rds-DNda7MnDzRs/evotypes/iq_transfer/aced-evotypes_transfer/.g3t/work/24.json --profile aced --upload-path /rds/project/rds-DNda7MnDzRs/evotypes/iq_transfer/aced-evotypes_transfer/ --bucket aced-ohsu-production --numparallel 75

#mySession34 LP6008340-DNA_H05.bam
tmux new -s mySession34
conda activate gen3_transfer
gen3-client upload-multiple --manifest /rds/project/rds-DNda7MnDzRs/evotypes/iq_transfer/aced-evotypes_transfer/.g3t/work/34.json --profile aced --upload-path /rds/project/rds-DNda7MnDzRs/evotypes/iq_transfer/aced-evotypes_transfer/ --bucket aced-ohsu-production --numparallel 75
```

**Improvements to Make**
- Resolve projects 
- resolve existing problems with upload to (waiting on exact error)
- Spec out the use case for uploading files in parallel -> 