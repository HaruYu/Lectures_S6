º---
title: "OS2"
author: [Vincent Trinh]
date: 15 Février 2018
...

# Operating system 1

* Numéro: 1
* Prof: Gabriel Laskaar
* Date: 15 février 2018

## Correction Contrôle
### what is the purpose of paging in a os?
Isoler les process entre eux, donner des autorisations

### How the pagefault handler of a modern operating system works?
Flemme d'écrire ce qu'il dit.

```
.section ksyms
Cette directive signifie rentrer dans la section ksyms
.size
La taille d'un symbole
```


***
# 22 février 2018
---
## Virtualisation, a quoi ça sert etc

* Machine virtuelle etc
Refaire marcher un système matériel

On virtualise à plein d'endroit : virtualisation de mémoire par exemple.
But: Exposer à l'utilisateur qqc qui ressemble a de la mémoire mais c'est pas la même chose pour isoler. Avoir au final des performances qui ont la même vitesse que s'il n'y a pas les couches.

Principe: Traduire les adresses d'une maniere ou d'une autre et elles se comportent comme les autres. C'est la même chose que la mémoire.

Ce qu'on veut faire:

* être capable de lancer un kernel en userland

Quand on execute un kernel en userland normalement, ca marche bien mais ca casse au bout d'un moment (très vite d'ailleurs). Il y a deux types de reistres: les types généraux et les types sensibles (de configuration) ils contiennent la config du processeur.
Instructions sensibles et générales. Sensible : lit et écrit dans un registre de configuration.
Instructions privilégiés: utilisables qu'en mode superviseur.
Ca va commencer a casser quand on utilise les instructions privilégiés.

Les devices: Un OS attend a avoir des devices.
Principe: Ca s'utilise plus ou moins de la même manière. Il y a des zones de RAM et des zones sur les devices.

Si on peut faire ça, alors l'architecture est virtualisable (a ce point du cours en tout cas)

POurquoi on virtualise? Pour le fric. On achète une machine et on met un service dessus. Quand on veut un autre service, on en achète une autre etc.

Ce serait bien de virtualiser sur des machines user friendly (aka x86)
Ce qu'ils font? On a des instructions sensibles non privilégiés. On lit les instructions a l'avance, et on les patch et on lance le tra.

Autre solution: Modifier l'OS. et ne pas appeler les instructions problematiques, et on les remplace par des hypercalls.
-> C'est de la triche. (qui est un fléau d'ailleurs.)

Conteneurs

***
# 07 mars 2018 : File Systems
---

## why do we need filesystems:

* Need more spaces bigger than virtual memory. RAM: there are not much and not persisting.
* Data persistence (in time)
* Data sharing between processes (which are separated from one to other)

## Vocabulary

* Filesystem: Format and logic to access storage (file as others but placed directly in the disk cf: ReadISO)
* Directory: List files
* File: unit of storage
* Block: Minimum part of a file (n blocks of a fixed size) those who are relative to the disk
* Partition: Part of a storage.

## How a disk works

The storing way is not the same in a disk as in RAM.
* Several blocks

* LBA (logical block access) offset of the block.
* Block size (usually 4K)
* Operations : read, right, flush (flush: sync the operations "from this point, everything before is done")
* Queues: submit queue, completion queue (operations we ask to do in submit queue). The OS does it and organises it take not necesarly the right order.


## Different medias

* Hard Drive (rotating) magnetic disks. Kind of slow
* Flash (SSD, ...) Non volatile address and directly accessible. advantage: Several requests can be done at the same time.

Protocols

* IDE (ATA): Try to send a request, wait if it works.
  - DMA : Direct Memory access. Hardware protocol that allows devices to talk with memory. No one knows which request is done / if anything is being done or anything -> it sucks
* SCSI : Protocols used in servers -not PCs- serial bus.
  - Can chain several disks.
  - A lot of current disks are using this protocol.
* SATA & SAS (sas is server version of SATA). Serial-ATA. in fact, a lot of SCSI commands are used with SATA.
* NVME Adapt to high transfer speed : scalable storage, efficient protocol and parallelisable
  - Namespaced : potentially Have several OS separated and usable at the same time
  - Every devices use the same driver.

memio : physical address that represent registers of devices
Serial VS. parallel transferts
Serial is easier to implement efficient things. + The frequency can be very high.
Parallel can transfer more data in the same time but has to synchronise it with the CPU >> slower.

## Filesystems

* A file has an unique identifier. (inode)
* Format: hint about the internal structure of the file
* Type
* Attributes:
  - Dates
  - Owner
  - ACLs
  - Archive
  - hidden

Types of files:
* MS-DOS: Only some files can be executed (com, exe, bat)
* MacOS: Information about application creator are stored in order to relaunch it on opening
* UNIX: No types (except for chardev, blockdev).
  - symlinks
  - block device, chardevice
  - socket
  - pipe

## Operation on files

Every files have the same operations. How's that? There are abstractions on it. A structure file has a function table pointer on it so it can be 'polimorph'

### mount(2)

put a block device in a file.

## Block

* Partition tables
  - MBR : Master boot Record
    - 1st block of the disk (512B)
      - Bootloader and partition table.
  - 4 partitions : 1 partition = 1 flag, type, begin LBA and nb of blocks in the partition.
  - EFI : agreement and do a spec for a firmware
    - 4 primary partitions
    - Extend partitions

***
# 08 mars 2018
---

There's a filesystem in the disk. There files can be stored. A header must be on the disk to know what's in

## Superblock

In the superblock there's a magick number that allows to identify the block. (as same as most elf etc.).

### Problems

This superblock is critical. That's why there might be redundancy.

Size of a superblock : Size of a block. Amount of inode in the filesystem, amount of files, amount of blocks, min size of file, max size of file...

## Inode

This is a structure. Composed of metadatas, a tab with addresses (direct blocks) and indirect blocks B-tree system (Addresses that points to other tabs of blocks), double indirect blocks same as indect but with height 2, and triple.
