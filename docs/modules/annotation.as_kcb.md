## Description


This experimental module annotates molecular features using results from the [KnownClusterBlast](https://docs.antismash.secondarymetabolites.org/modules/clusterblast/) algorithm of the popular genome annotation tool [antiSMASH](https://antismash.secondarymetabolites.org). KnownClusterBlast performs a multigene BLAST comparison against entries in the [MIBiG repository](https://mibig.secondarymetabolites.org/), and registers significant hits with a score of percent similarity. The FERMO module takes the antiSMASH output, parses the KnownClusterBlast matches, selects matches exceeding a certain similarity score, and extracts the metabolites experimentally associated with the MIBiG entries. From this subset of molecules, a targeted in silico MS/MS spectral library is created using [CFM-ID](https://cfmid.wishartlab.com/) and used for spectral library matching (for more information, see [fermo_core_extras](https://github.com/mmzdouc/fermo_core_extras). The assumption is that if two genomes contain two similar biosynthetic gene clusters (BGCs), the metabolites resulting from these two BGCs should also show chemical similarity, with similar MS/MS fragmentation that should allow spectral matching. Matches would likely be analogs (not exact matches), but could nevertheless help to annotate a feature.

## Parameters `modified cosine`

- `fragment_tol`: the absolute tolerance for matching two MS/MS fragments, in m/z units.
- `min_nr_matched_peaks`: minimum number of fragments that must be matched between two MS/MS fragmentation spectra.
- `score_cutoff`: minimum score to consider a match
- `max_precursor_mass_diff`: maximum allowed difference between precursor m/z of feature and library m/z.

## Parameters `ms2deepscore`

- `score_cutoff`: minimum score to consider a match
- `max_precursor_mass_diff`: maximum allowed difference between precursor m/z of feature and library m/z.


## Limitations

- Currently, this module accepts a single antiSMASH results folder from the analysis of a single genome. Therefore, all LC-MS samples annotated by this method must also derive from the organism the genome is associated with. In the future, this will be expanded to multiple genomes as well. 
- The definition of similarity in the context of BGCs: while it is assumed that two similar BGCs should produce similar metabolites, there are many exceptions, and there are cases where a single BGC can produce chemically very different molecules. 
- All spectra in the MIBiG spectral library were generated by in silico MS/MS fragmentation, given the poor coverage with experimentally generated spectra. In silico fragmentation prediction may not work equally well for all types of molecules and may lead to false positive and false negative matches. Therefore, caution in the interpretation of results is advised. In the future, the in silico generated spectral library may be replaced with experimentally spectra.
