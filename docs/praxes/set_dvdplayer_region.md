# Set a DVD Player's Region from Linux (Debian based)

Many DVD players have manufacturer limits in the firmware. Mine had a limit of 5 region resets.

There are 8 regions. You probably want a US region.

If you always need more than one region you will need multiple DVD drives.

In 2017, DVD drives are practically without value.

## Procedure

Use the regionset utility to change the region. If you run out of resets, the DVD player keeps the final region you selected.  Some DVD players may have firmware upgrades that reset the counter.

1. `apt install regionset`
2. Run `regionset` and set the region if it is not already set.



