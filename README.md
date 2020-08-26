# Get data from the Human Connectome Project Open Access dataset with DataLad

[![made-with-datalad](https://www.datalad.org/badges/made_with.svg)](https://datalad.org)

This dataset enables data retrieval with DataLad (0.12.2 or later) from the
[HCP Open Access dataset](https://registry.opendata.aws/hcp-openaccess/) for users
that accepted the WU-Minn HCP Consortium Open Access Data Use Terms and obtained
valid AWS credentials via [db.humanconnectome.org](http://db.humanconnectome.org).

## Human Connectome Project

The Human [Connectome Project (HCP)](http://www.humanconnectomeproject.org/about/)
aims to construct a map of the complete structural and functional neural
connections in vivo within and across individuals.

Its 'WU-Minn HCP Open Access Data' data release includes high-resolution 3T MR
scans from young healthy adult twins and non-twin siblings (ages 22-35) using
four imaging modalities: structural images (T1w and T2w), resting-state fMRI (rfMRI),
task-fMRI (tfMRI), and high angular resolution diffusion imaging (dMRI). It
further includes behavioral and other individual subject measure data for all,
and MEG data and 7T MR data for a subset of subjects (twin pairs).

## Data access and retrieval with DataLad

To retrieve HCP Open Access data via DataLad with this dataset, you need to agree
to the [WU-Minn HCP Consortium Open Access Data Use Terms](./DATA_USE_AGREEMENT.md)
and obtain valid AWS credentials:

- Create an account at http://db.humanconnectome.org.
- Log into your account and accept the data use terms of the "WU-Minn HCP Data -
  1200 Subjects" data release.
- Enable Amazon S3 access for your Amazon account to get an access key ID
  and a secret access secret key (click on the button with the S3 logo).
  - The access key ID is a character string similar to this: ``AKIAXOX5CT57GHZ4SVFV``
  - The secret access key is a character string similar to this: ``vntFcVA+YI0Ii3tVZPpdyQrgp2H05YjesyXKGE+n``

You will be asked to supply your AWS credentials the first time you use `datalad get`
to retrieve file content of your choice from
the [HCP Open Access dataset](https://registry.opendata.aws/hcp-openaccess/). You
should only need to provide credentials once, and all subsequent `datalad get` commands
will retrieve data without asking them again.

Note that a subset of files is not available via the S3 bucket and is instead
retrieved from the ConnectomeDB database.
This concerns the following files:

- HCP1200/{205199,200614}/MNINonlinear/Results/rfMRI_REST1_LR/rfMRI_REST1_LR.nii.gz
- HCP1200/199251/MNINonlinear/Results/rfMRI_REST2_RL/rfMRI_REST2_RL.nii.gz
- HCP1200/{150928,198451}/MNINonlinear/Results/rfMRI_REST2_RL/rfMRI_REST2_RL_hp2000_clean.nii.gz
- HCP1200/{150928,208226}/MNINonlinear/Results/rfMRI_REST1_RL/rfMRI_REST1_RL_hp2000_clean.nii.gz
- HCP1200/{150928,202820,213421}/MNINonlinear/Results/rfMRI_REST2_LR/rfMRI_REST2_LR_hp2000_clean.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_WM_LR/tfMRI_WM_LR.nii.gz
- HCP1200/{150928,668361}/MNINonlinear/Results/tfMRI_WM_RL/tfMRI_WM_RL.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_GAMBLING_RL/tfMRI_GAMBLING_RL.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_MOTOR_LR/tfMRI_MOTOR_LR.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_MOTOR_RL/tfMRI_MOTOR_RL.nii.gz
- HCP1200/{150928,214524}/MNINonlinear/Results/tfMRI_LANGUAGE_LR/tfMRI_LANGUAGE_LR.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_LANGUAGE_RL/tfMRI_LANGUAGE_RL.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_SOCIAL_LR/tfMRI_SOCIAL_LR.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_SOCIAL_RL/tfMRI_SOCIAL_RL.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_EMOTION_LR/tfMRI_EMOTION_LR.nii.gz
- HCP1200/150928/MNINonlinear/Results/tfMRI_EMOTION_RL/tfMRI_EMOTION_RL.nii.gz


When retrieving the files listed above, you will be asked to supply your ConnectomeDB credentials
(user name and password) instead of your AWS credentials.
As with AWS credentials, you will only need to supply these credentials once.

## Dataset structure

Each ``HCP1200/`` subject directory in this dataset is a DataLad subdataset. The
command `datalad get -n <subject-id>` clones this subdataset and allows to
access this subjects release notes (subdirectory `release-notes`). Within each
subject's subdataset, one DataLad subdataset exists for each additional
available subdirectory (e.g., ``MEG``, ``T1w``, etc., as far as available
for the particular subject).

If you have never used [DataLad](https://www.datalad.org/) before, please read the
section on DataLad datasets below.

## DataLad datasets and how to use them

This repository is a [DataLad](https://www.datalad.org/) dataset. It allows fine-grained
data access up to the level of single files of the HCP Open Access dataset without hosting
the HCP data. In order to use this repository for data retrieval,
[DataLad](https://www.datalad.org/) is required. It is a free and open source command line
tool, available for all major operating systems, and builds up on Git and
[git-annex](https://git-annex.branchable.com/) to allow sharing, synchronizing, and version
controlling collections of large files. You can find information on how to install DataLad
at [handbook.datalad.org/en/latest/intro/installation.html](http://handbook.datalad.org/en/latest/intro/installation.html).

### Get the dataset

A DataLad dataset can be `cloned` by running

```
datalad clone <url>
```
Once a dataset is cloned, it is a light-weight directory on your local machine.
At
this point,
it contains only small metadata and information on the identity of the files in the dataset,
but not actual *content* of the (sometimes large) data files.

### Retrieve dataset content

After cloning a dataset, you can retrieve file contents by running
```
datalad get <path/to/directory/or/file>
```
This command will trigger a download of the files, directories, or subdatasets you have specified.

DataLad datasets can contain other datasets, so called *subdatasets*. If you clone the top-level
dataset, subdatasets do not yet contain metadata and information on the identity of files,
but appear to be empty directories. In order to retrieve file availability metadata in
subdatasets, run

```
datalad get -n <path/to/subdataset>
```
Afterwards, you can browse the retrieved metadata to find out about subdataset contents, and
retrieve individual files with `datalad get`. If you use `datalad get <path/to/subdataset>`,
all contents of the subdataset will be downloaded at once.

### Stay up-to-date

DataLad datasets can be updated. The command `datalad update` will *fetch* updates and store them
on a different branch (by default `remotes/origin/master`). Running
```
datalad update --merge
```
will *pull* available updates and integrate them in one go.

### More information

More information on DataLad and how to use it can be found in the DataLad Handbook at
[handbook.datalad.org](http://handbook.datalad.org/en/latest/index.html). The chapter
"DataLad datasets" can help you to familiarize yourself with the concept of a dataset.
