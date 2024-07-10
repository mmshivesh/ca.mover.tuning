# Mover Tuning

## About

This is a simple [Unraid](https://unraid.net/) plugin that will let you fine-tune the operation of the [mover](https://docs.unraid.net/unraid-os/manual/additional-settings/#mover).

- On scheduled runs of mover
    - Only actually move file(s) if the the cache drive is getting full (selectable threshold)
    - Optionally don't move if a parity check / rebuild is already in-progress
- Optional ability to completely disable the scheduled runs of mover
- Manually executed runs of mover ("Move Now" button) can either follow the rules for schedules, or always move all files

This repo merge all [pull requests](https://github.com/hugenbd/ca.mover.tuning/pulls) after review from [Hugenbd's repo](https://github.com/hugenbd/ca.mover.tuning) (cosmetics, merge skipfiletypes from shares, 4 changes from Swarles below) and add several feature, as for example automatic age threshold and compatibility with Unraid 7.x, and other stuff coming.

## Changelog
- 2024-07-10
    - [Unraid 7.0.0 compatibility](https://github.com/R3yn4ld/ca.mover.tuning/tree/unraid-7.0.0-compatibility) ([R3yn4ld](https://github.com/R3yn4ld)): Correct "move now without mover tuning plugin" bug (R3yn4ld)

- 2024-07-07:
    - [Unraid 7.0.0 compatibility](https://github.com/R3yn4ld/ca.mover.tuning/tree/unraid-7.0.0-compatibility) ([R3yn4ld](https://github.com/R3yn4ld))

- 2024-06-30: 
    - [Automatic age threshold](https://github.com/R3yn4ld/ca.mover.tuning/tree/automatic-age-threshold) ([R3yn4ld](https://github.com/R3yn4ld))
    - [Minor spelling corrections & README](https://github.com/dphelan/ca.mover.tuning/tree/spelling-corrections) ([Dphelan](https://github.com/dphelan))
    - [Merge share skipfiletypes](https://github.com/davendesai/unraid-mover-tuning/tree/merge-share-skipfiletypes) ([Davendsai](https://github.com/davendesai))(add/merge per share skipfilestype to global skips)
    - [Update Mover.tuning.page](https://github.com/Squidly271/ca.mover.tuning/tree/patch-2) ([Squid](https://github.com/Squidly271))

- 2023.12.19 (was not in [master branch from hugenbd](https://github.com/hugenbd/ca.mover.tuning))
    - [4 changes from Swarles](https://github.com/hugenbd/ca.mover.tuning/commit/64e06e91bd83431d768346e4d8158f7be039564e) ([Swarles](https://forums.unraid.net/profile/213067-swarles/))
        - Change "while read" lines in age_mover to "while IFS= read -r" to fix trailing white spaces (Swarles)
        - Fix where sometimes mover would not run to mover.old scrip (Swarles)
        - Log if "share.cfg" doesn't exists to help trouble shooting (Swarles)
        - Check for ca.mover.tuning.cfg file and additional logging. (Swarles)

## Installation

You can download and install plugins with [Community Apps](https://unraid.net/community/apps/c/plugins).

## Configuration

You'll find its settings within Settings - [Scheduler](https://docs.unraid.net/unraid-os/manual/additional-settings/#scheduler).

## Usage

After installation, the default settings are set so that there is no difference from Unraid's normal mover operations.

See the [_Mover Tuning_ thread on the Unraid support forum](https://forums.unraid.net/topic/70783-plugin-mover-tuning/) for more details and discussions.

## Thanks

This was originally created by [Squid](https://github.com/Squidly271) and updated by [hugenbd](https://github.com/hugenbd/ca.mover.tuning), with contributions by [Castcore](https://github.com/Castcore), [Swarles](https://github.com/hugenbd/ca.mover.tuning/commit/64e06e91bd83431d768346e4d8158f7be039564e), [Dphelan](https://github.com/dphelan) and [Davendsai](https://github.com/davendesai).
