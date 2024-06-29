# Mover Tuning

## About

This is a simple [Unraid](https://unraid.net/) plugin that will let you fine-tune the operation of the [mover](https://docs.unraid.net/unraid-os/manual/additional-settings/#mover).

- On scheduled runs of mover
    - Only actually move file(s) if the the cache drive is getting full (selectable threshold)
    - Optionally don't move if a parity check / rebuild is already in-progress
- Optional ability to completely disable the scheduled runs of mover
- Manually executed runs of mover ("Move Now" button) can either follow the rules for schedules, or always move all files

This plugin was originaly developped by [Squid](https://github.com/Squidly271), [Castcore](https://github.com/Castcore), [Hugenbdd](https://github.com/hugenbd), with contribution from [Dphelan](https://github.com/dphelan), and [Davendsai](https://github.com/davendesai).
V2 merge all [pull requests](https://github.com/hugenbd/ca.mover.tuning/pulls) from [V1 repo](https://github.com/hugenbd/ca.mover.tuning) and will add several feature, as for example automatic age threshold

## Installation

You can download and install plugins with [Community Apps](https://unraid.net/community/apps/c/plugins).

## Configuration

You'll find its settings within Settings - [Scheduler](https://docs.unraid.net/unraid-os/manual/additional-settings/#scheduler).

## Usage

After installation, the default settings are set so that there is no difference from Unraid's normal mover operations.

See the [_Mover Tuning_ thread on the Unraid support forum](https://forums.unraid.net/topic/70783-plugin-mover-tuning/) for more details and discussions.

## Thanks

This was originally created by [Squid](https://github.com/Squidly271) and updated by [hugenbd](https://github.com/hugenbd/ca.mover.tuning), with contributions by [Castcore](https://github.com/Castcore) and [Swarles](https://github.com/hugenbd/ca.mover.tuning/commit/64e06e91bd83431d768346e4d8158f7be039564e).
