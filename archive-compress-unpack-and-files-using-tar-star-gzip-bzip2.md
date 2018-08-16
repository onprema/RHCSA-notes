## Archive, Compress, Unpack and Uncompress Files Using tar, star, gzip and bzip2

- `tar` does not do compression, it just creates archives. it relies on a 3rd party, like `gzip` for compression.

- `gzip FILE` compresses FILE and renames it FILE.gz
- `gunzip FILE.gz` decompresses FILE and renames it FILE

- you cannot compress a DIRECTORY with `gzip` so you need to create an archive, which is just a grouping of all the files in a directory, basically.

- `tar -cvf FILE.tar` creates an archive called FILE (not compressed)
- `tar -cvzf FILE.tar.gz` creates a compressed archive using gzip (-z flag)

- by default, when you extract a compressed archive with `tar -xvf FILE.tar.gz`, it will overwrite any file with the same name. to avoid issues you can use a flag (-d): `tar -dvf FILE.tar.gz` which will display the DIFF (d for DIFF) between whats in the archive and whats on the current system which will display the DIFF (d for DIFF) between whats in the archive and whats on the current system.

- `star` (which is not installed on RHEL by default) can be used for large data sets. And it doesn't overwrite files that are newer than the files in the archive. It gives us more protection!
