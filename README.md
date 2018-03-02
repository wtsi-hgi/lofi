# Lo-Fi

Downsample alignment data (SAM, BAM or CRAM files) given specific
constraints.

# Requirements

* GNU Awk
* [Samtools](http://www.htslib.org/) 1.?

# Usage

    lofi [--coverage COVERAGE] [--species SPECIES]
         [--read-groups RG_RANGE] [--rg-coverage RG_COVERAGE] [--keep-rg RG]
         [--strategy STRATEGY] [--tolerance TOLERANCE] [--seed SEED]
         [--prefix PREFIX] [--no-recombine]
         INPUT

At least one constraint must be specified.

## Coverage Constraints

    --coverage COVERAGE        The overall coverage of the output
    --rg-coverage RG_COVERAGE  The minimum coverage in output read groups

`COVERAGE` and `RG_COVERAGE` are specified as the number of base pairs,
optionally suffixed with `k`, `M` or `G`. If the `--species` option is
used, an `x` suffix may also be used, indicating a coverage relative to
the species genome size.

Supported `SPECIES` values:
* `human`
* `mouse`
* `zebrafish`

## Read Group Constraints

    --read-groups RG_RANGE     Read groups in the output
    --keep-rg RG               Do not drop the read group with the given ID;
                               this can be specified multiple times

The `RG_RANGE` takes the format `MIN-`, `-MAX`, `MIN-MAX` or `EXACT`.

## Downsampling Options

    --strategy STRATEGY        Downsampling strategy [default: DROP_RG]
    --tolerance TOLERANCE      Allowed percentage difference in output
                               coverage from target [default: 10]
    --seed SEED                Random seed [default: 0]

Supported `STRATEGY` values:
* `DROP_RG`: Prefer dropping read groups over downsampling reads

## Output Options

    --prefix PREFIX            Output path prefix
    --no-recombine             Don't recombine individual read groups

The output file(s) will be named `[PREFIX]INPUT[.READ_GROUP].downsampled`,
where `READ_GROUP` will be the read group ID if `--no-recombine` is
specified. The `PREFIX`, if specified, is relative to the `INPUT`'s
location, or an absolute path.
