# XLMOD Ontology
The XLMOD ontology is a structured, controlled vocabulary for cross-linking reagents and cross-linker related post-translational modifications used in cross-linking mass spectrometry experiments and derivatization reagents for GC-MS. Developed by the HUPO Proteomics Standards Initiative (PSI).

Its previous home was at within the mzIndentML repository at https://github.com/HUPO-PSI/mzIdentML/tree/master/cv
but as of 2022-02-04 has been given its own home here.

The draft mapping file for the mzTab validator can be found at https://raw.githubusercontent.com/nilshoffmann/mzTab/580489542e89f4cf0d2925fda683ef2963f1e883/specification_document-developments/2_0-Metabolomics-Draft/mzTab_2_0-M_mapping.xml


## Other Information

Additional semi-structured information about xmlmod can be found at: https://github.com/HUPO-PSI/xlmod-CV/blob/main/xlmod.md


## Requesting a new term

Anyone can request a new term be added to the controlled vocabulary by opening an issue or a pull
request against this repository. We'd appreciate any help you can contribute when submitting a new
term, from proposing the term name and description to defining its relationships and properties. Submitting
the request already formatted as an OBO term is helpful too! Don't worry about finding an unused id string,
that can be handled near the end.

If you're requesting multiple related terms, you can submit them in a single issue/pull request.

## Syntax for rules

| Property value | Type | Syntax | Explanation | Examples |
| --- | --- | --- | --- | --- |
| bridgeFormula | xsd:string | Molecular formula, see below | The formula of the modification when bound to at least two amino acids. | `C7 D10 H2 N4` `-C1 -H2 O1` `13C6 H6 O2` |
| deadEndFormula | xsd:string | Molecular formula, see below | The formula of the modification when bound to one amino acid, the other end is neutralised and this neutralising agent is included in the formula. | `C28 H41 N6 O11 S1` |
| monoIsotopicMass | xsd:double | number | The monoisotopic mass of the formula (deadEnd or bridge depending on the entry). | `-2.01565007` `156.07864431` |
| neutralLossFormula | xsd:string | Molecular formula, see below | A neutral loss from the full cross-linker. Any negative occurrences indicate something that leaves the cross-linker. So `-H2 -O1` indicate a neutral loss of water.  | `-H2 -O1` `-H3 -N1` |
| reactionSites | xsd:nonNegativeInteger | number | The number of reaction sides on this cross-linker, can be 1, 2, 3, or even higher. | `1` `2` `3` |
| specificities | xsd:string | Sites are separated by an ampersand `&`. Each site has a list of possible peptide locations separated by commas and wrapped in brackets. | These are the locations where this cross-linker binds. If only one site is given (no ampersand is present) but `reactionSites` is 2 the reaction sides both have the same specificity. | `(C)&(C)` `(K,Protein N-term)` |
| secondarySpecificities | xsd:string | See above | These are the locations where this cross-linker can also bind but has a much lower rate. | `(S,T,Y)` |
| baseSpecificities | xsd:string | Sites are separated by an ampersand `&`. Each site has a list of possible DNA locations separated by commas and wrapped in brackets. | These are the locations where this cross-linker binds. If only one site is given (no ampersand is present) but `reactionSites` is 2 the reaction sides both have the same specificity. | `(Guanine)` |
| secondarybaseSpecificities | xsd:string | See above | These are the locations where this cross-linker can also bind but has a much lower rate. | `(Adenine, Cytosine)` |
| stubDefinition | xsd:string | A list of fragmentation techniques followed by an equals sign `=`, followed by a formula indicating the first stub, possibly followed by a list of possible neutral losses each preceded by a comma, followed by a colon `:` followed by a formula denoting the second stub, again possibly followed by neutral losses. | This indicates the possible stubs that can be generated when doing mass spectrometry fragmentation. Multiple definitions can be given for each cross-linker to indicate different stubs. A stub formula can be empty if no modification is left at that site. | `CID = H4 C3 O2 S1, -H2 -O1 : H2 C3 O1` `ETD = -H1 : ` |
| spacerLength | xsd:float | number | This indicates the length of the linker in angstrom. | `7.7` |
| minSpacerLength | xsd:float | number | This indicates the minimal length of the linker in angstrom. | `5.0` |
| maxSpacerLength | xsd:float | number | This indicates the maximal length of the linker in angstrom. | `20.0` |
| doubletDeltaMass | xsd:double | number | The difference in mass between stubs. | `5.0168` |
| hydrophilicPEGchain | xsd:nonNegativeInteger | number | The length of the PEG chain. | `3` |
| reporterMass | xsd:double | number | The mass of a diagnostic ion. | `555.2481` |
| maxAbsorption | xsd:string | Number followed by a space followed by the unit (`nm`) | Peak of the absorption spectrum. | `236 nm` |
| waveLengthRange | xsd:string | Two numbers separated by a hyphen `-` followed by a space followed by the unit (`nm`). Or the name of a wavelength range (eg `UV`). | Range of wavelengths that are absorbed by the cross-linker. | `250-350 nm` `UV` |

### Molecular formula
Element symbols followed by their occurrence, each element is separated by spaces. Negative occurrence is indicated by starting the element block with a minus. Isotopes are indicated by writing the isotope number before the element, behind a minus if the occurrence is negative. `D` is allowed as element indicating deuterium or `2H`.

```
C7 D10 H2 N4
-C1 -2H2 O1
13C6 H6 O2
```