# Pipeline patches (not yet applied on the Mac)

Changes Claude made to the shared Blender pipeline (`~/Desktop/Friendzy/Blender/`) in cloud sessions, kept here so
they aren't lost before they're applied. The pipeline itself still lives only in the Friendzy folder.

- `blender.patch`: every change, against the `blender-code.zip` uploaded on 29 Oct. Apply inside the Blender folder:
  `cd ~/Desktop/Friendzy/Blender && git apply ~/Desktop/Porchlight/pipeline-patches/blender.patch`
  (or `patch -p1 < .../blender.patch` if the folder isn't a git checkout). Then run `python3 doctor.py`.
- `CHANGES.md`: what changed and why, in plain words.

The patch is updated as more work lands; it always holds everything since that zip.
