# CommitLint

People (myself included) sometimes do crazily stupid things to their repo.

Maybe because of the lack of knowledge, maybe because they are in a hurry, and
operate repo without first reaching a state of mental clarity.

In any case, some of those bad deeds goes undiscovered, for months, while
commits keeps rolling in, and pile up like a small montain.

And one day, the hidden mine explodes, and undo the damage is next to impossible.

This project aims to sanitize the commits, detect and reject those operations that
are just [plain out wrong](#Enforced_Rules).

It exposes the problem early so that correction are relatively painless, at least
compared to the alternatives described above.

## Assumptions

1. You use annotated tags for marking release versions.
2. Tagging scheme follows the requirements of the [VersionLint](https://github.com/Adam5Wu/VersionLint) utility.

## Enforced Rules

1. Tag prefix does not conform to VersionLint requirement

  Error message sample:
  ```
  ERROR: New tag 'x1.1' does not use an acceptable prefix
  ```
2. Two releases with different versions (i.e. tags) CANNOT be on the same commit

  Error message sample:
  ```
  ERROR: New tag 'v2.0' collides with existing tag 'v1.0"
  ```
3. Merge done in [the wrong direction](http://www.bradapp.com/acme/branching/pitfalls.html#WrongWayMerge)

  Error message sample:
  ```
  - Commit: 33b64cd737bb8418c719890953dd0b1e2c26205f
    Natrual parent 84f5b9b740a8673ef18fa5316c979822506cc20d, tag: v1.1
    Foreign parent 33b64cd737bb8418c719890953dd0b1e2c26205f, tag: v2.0
    ERROR: Detected wrong way merge: 1.1 < 2.0
  ```
  
## How To Use

Place the "custom_hooks" under the remote Git projects' root.
