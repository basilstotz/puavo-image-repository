# Puavo Image Repository

This document describes how run to your own Puavo Image Repository.

### Why?
But why would you wand to run your own repostiory? You might want
* that your user only acces a repository which runs (e.g. for privacy reasons) under your local jurisdiction.
* that the load of the main repository decreases
* to use modified or extend version of Puavo-OS 

### Requirements

A Puavo Image Repository is just a plain https service, which is only serving static files. So any server with enough disc space (~500 Gbyte) will do the job. Be aware, that the generation of the rdiff-files is very cpu/io intensive so it might be reasonable to prepare your date offline, only  uploading the final data to the server.  

### Offline Data Preparation

Let's assume we want to expose the following images for the clients:

```
puavo-os-images
├── puavo-os-amxa-buster-2021-04-13-192449-amd64.img
├── puavo-os-amxa-buster-2021-04-13-193910-amd64.img
├── puavo-os-amxa-buster-2022-01-17-120001-amd64.img
├── puavo-os-amxa-buster-2022-01-20-173248-amd64.img
└── puavo-os-free-buster-2022-02-04-140532-amd64.img
```
For ensure the integrity of the data and to spped up the update process of clients some additional file have to be generated:
* A **cheksum** file.
* Some  **meta** files.
* And, of course, the **rdiff** files.

This might look like this:

```
mirror
├── CKSUMS
├── meta
│   ├── puavo-os-amxa-buster-amd64.json
│   └── puavo-os-free-buster-amd64.json
├── puavo-os-amxa-buster-2021-04-13-192449-amd64.img
├── puavo-os-amxa-buster-2021-04-13-193910-amd64.img
├── puavo-os-amxa-buster-2022-01-17-120001-amd64.img
├── puavo-os-amxa-buster-2022-01-20-173248-amd64.img
├── puavo-os-free-buster-2022-02-04-140532-amd64.img
└── rdiffs
    ├── puavo-os-amxa-buster-2021-04-13-192449--2021-04-13-193910-amd64.rdiff
    ├── puavo-os-amxa-buster-2022-01-17-120001--2022-01-20-173248-amd64.rdiff
    └── puavo-os-amxa-buster-2022-01-20-173248--2022-01-17-120001-amd64.rdiff
```
The creation of these additional files is an integral part of PuavoOS and can be done on every Puavo installation (of course  it can also be done on non PuavoOS oss's)

#### On PuavoOS
When your images are in **puavo-os-images** and your mirror will reside in **mirror**. You just call (the binary in this repo!):

```
# puavo-update-repository puavo-os-images mirror
```

Now, just wait (some hours) and enjoy your updated repository.

#### On other Platforms

Other platforms lack the PuavoOS installation. So just do

```
$ git clone https://github.com/puavo-org/puavo-os.git
```

and call puavo-update-repository with

```
# puavo-update-repository --puavo-os path/to/puavo-os puavo-os-images mirror
```

That's it(for now).
