# MEALR combinatorial regulation analysis
## Extract TRANSFAC(R) PWMs from combinatorial regulation analysis
This tool extracts TRANSFAC&#174; PWMs from a result table generated by the <a href="https://platform.genexplain.com/bioumlweb/#de=analyses/Methods/MEALR%20combinatorial%20regulation%20analysis/TRANSFAC(R)%20MEALR%20combinatorial%20regulation%20analysis">MEALR combinatorial regulation analysis</a>.
The PWMs represent transcription factor binding specificities that constitute the combinatorial
module predicted by the MEALR model.

**Input parameters**

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Input MEALR search table</td>
<td>Input table, a MEALR search result table</td>
</tr>
<tr>
<td>Probability cutoff</td>
<td>Probability cutoff</td>
</tr>
<tr>
<td>Accuracy cutoff</td>
<td>Model accuracy cutoff</td>
</tr>
<tr>
<td>Importance cutoff</td>
<td>Logistic regression coefficient cutoff</td>
</tr>
<tr>
<td>Output</td>
<td>Output table</td>
</tr>
</tbody>
</table>
Probability and accuracy cutoffs select MEALR models from the input table based on the observed
match probability and the model accuracy on test data, respectively. The importance cutoff is
applied to the PWM feature coefficients of the MEALR model allowing to focus on more important
matrices by increasing the threshold.

**Output**

The output contains the TRANSFAC&#174; PWMs extracted from MEALR models according to specified
cutoffs. This table can further be applied in several analyses, e.g. to extract corresponding
transcription factors using the tool <a href=""></a> or to create a profile for binding site
predictions (<a href="https://platform.genexplain.com/bioumlweb/#de=analyses/Methods/Site%20analysis/Create%20profile%20from%20site%20model%20table">
Create profile from site model table</a>) with <a href="https://platform.genexplain.com/bioumlweb/#de=analyses/Methods/Site%20analysis/TRANSFAC(R)%20Match(TM)%20for%20tracks">MATCH<sup>TM</sup></a>.

<table>
<thead>
<tr>
<th>Output table column</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Max. probability</td>
<td>Highest match probability of models from which PWM was extracted</td>
</tr>
<tr>
<td>Max. accuracy</td>
<td>Highest accuracy of a model from which PWM was extracted</td>
</tr>
<tr>
<td>Max. importance</td>
<td>Highest importance of PWM in extracted models</td>
</tr>
<tr>
<td>Avg. probability</td>
<td>Average match probability of models from which PWM was extracted</td>
</tr>
<tr>
<td>Avg. accuracy</td>
<td>Average accuracy of a model from which PWM was extracted</td>
</tr>
<tr>
<td>Avg. importance</td>
<td>Average importance of PWM in extracted models</td>
</tr>
<tr>
<td>Min. probability</td>
<td>Lowest match probability of models from which PWM was extracted</td>
</tr>
<tr>
<td>Min. accuracy</td>
<td>Lowest accuracy of a model from which PWM was extracted</td>
</tr>
<tr>
<td>Min. importance</td>
<td>Lowest importance of PWM in extracted models</td>
</tr>
<tr>
<td>Cell sources</td>
<td>Cell sources of extracted models</td>
</tr>
<tr>
<td>Tissue sources</td>
<td>Tissue sources of extracted models</td>
</tr>
<tr>
<td>Factors</td>
<td>Transcription factors targeted in experiments of extracted models</td>
</tr>
<tr>
<td>Model ids</td>
<td>Ids of models from which PWM was extracted</td>
</tr>
</tbody>
</table>

**Example analysis**
<a href="https://platform.genexplain.com/bioumlweb/#de=analyses/Methods/MEALR%20combinatorial%20regulation%20analysis/Extract%20TRANSFAC(R)%20PWMs%20from%20combinatorial%20regulation%20analysis">Open</a> the tool in the user interface.

- Specify a result table of a MEALR search analysis ([Input example](https://platform.genexplain.com/bioumlweb/#de=data/Examples/Combinatorial%20regulation%20analysis%20of%20TAL1/Data/TAL1)).
- Specify probability, accuracy and importance cutoffs
- Specify an output table. A result path is suggested automatically on the basis of specified input (<a href="https://platform.genexplain.com/bioumlweb/#de=data/Examples/Combinatorial%20regulation%20analysis%20of%20TAL1/Data/TAL1">Example result</a>).

## TRANSFAC(R) MEALR combinatorial regulation analysis

This analysis applies combinatorial regulatory models (CRMs) based on the
<a href="#de=analyses/Methods/Site%20analysis/MEALR%20(tracks)">MEALR affinity score</a> &#91;<a href="#ref1">1</a>&#93;
to classify or scan sequences for occurrences of combinations of transcription factor binding sites
represented by TRANSFAC&#174; PWMs. The models are taken from the MEALR library whose training data
originate from the TRANSFAC&#174; collection of high-throughput sequencing experiments.

**Input parameters**

<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence track</td>
<td>Sequence track or collection to search</td>
</tr>
<tr>
<td>Sequence source</td>
<td>Sequence source associated with the sequence track. Either a custom or genomic sequence source</td>
</tr>
<tr>
<td>Cell sources</td>
<td>Focus on models from selected cell sources</td>
</tr>
<tr>
<td>Tissue sources</td>
<td>Focus on models from selected tissue sources</td>
</tr>
<tr>
<td>Classification mode</td>
<td>Classify entire sequence instead of scanning for hits</td>
</tr>
<tr>
<td>Scan mode</td>
<td>Scan mode, best hit or cutoff based</td>
</tr>
<tr>
<td>Step size</td>
<td>Step size for scanning mode</td>
</tr>
<tr>
<td>Probability cutoff</td>
<td>Cutoff for the probability that a sequence matches the model</td>
</tr>
<tr>
<td>Model accuracy cutoff</td>
<td>Select models with test set accuracy equal or better than the accuracy cutoff prior to search</td>
</tr>
<tr>
<td>Output folder</td>
<td>Output folder for analysis results</td>
</tr>
</tbody>
</table>


**Classification and scan modes**

The _Classification mode_ evaluates input sequences as a whole, whereas the _scan mode_ analyzes
sequence windows separated by the given _step size_ (sliding window). In scan mode, the _Best hit_
method reports the best scoring sequence window disregarding a cutoff and the _Cutoff_ method
reports the best non-overlapping windows satisfying the specified cutoff.

**Note**

The _MEALR search_ applies sequence length limits. The minimal sequence length for _scan_ **and**
_classification_ modes is **50** base characters. The _classification_ mode supports sequences up to
**5000** base characters.
Ideally, input sequences for _classification_ mode should have lengths corresponding to genomic
regions typically observed in ChIP-seq studies like 500 - 1000 bases, whereas input sequences for
scanning should not be too short, e.g. &ge;300 bases. We recommend to take differences between
model length and sequence length, which are reported in the output table, into account in the
assessment of the reliability of predictions.

Cell and tissue sources can be selected to focus on a subset of CRMs which have been trained with
data from respective sources. Please note that selection of multiple cells and/or tissues gathers
all CRMs that are associated with any one of selected sources.

**Output**

The output folder encompasses a table and sequence track with information about model hits.
The output table contains sequence start and end points of hits, model ids, match probabilities as
well as other values as described below. For input sequences derived from genomic regions &#40;instead
of imported as custom sequences&#41; the table includes in addition a sequence id generated for a
region as well as the genomic sequence id, start and end coordinates.

<table>
<thead>
<tr>
<th>Output table column</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Sequence id</td>
<td>Sequence id of custom or genomic sequence</td>
</tr>
<tr>
<td>Interval site name</td>
<td>Sequence id constructed for genomic interval</td>
</tr>
<tr>
<td>Start</td>
<td>CRM region start (one-based)</td>
</tr>
<tr>
<td>End</td>
<td>CRM region end (one-based)</td>
</tr>
<tr>
<td>Model id</td>
<td>MEALR model id</td>
</tr>
<tr>
<td>Factor gene</td>
<td>Gene symbol of transcription factor analyzed in source experiment generating training data</td>
</tr>
<tr>
<td>Cell source</td>
<td>Cell source of training data</td>
</tr>
<tr>
<td>Tissue source</td>
<td>Tissue source of training data</td>
</tr>
<tr>
<td>Model accuracy</td>
<td>Test set accuracy of MEALR model</td>
</tr>
<tr>
<td>Model type</td>
<td>Type of MEALR model (LR: logistic regression, WLR: LR with weighting of CRM region positions)</td>
</tr>
<tr>
<td>Model length</td>
<td>Length of CRM region</td>
</tr>
<tr>
<td>Sequence length</td>
<td>Length of analyzed sequence</td>
</tr>
<tr>
<td>Score</td>
<td>CRM score</td>
</tr>
<tr>
<td>Probability</td>
<td>CRM probability</td>
</tr>
</tbody>
</table>


**Example analysis**

<a href="https://platform.genexplain.com/bioumlweb/#de=analyses/Methods/MEALR%20combinatorial%20regulation%20analysis/TRANSFAC(R)%20MEALR%20combinatorial%20regulation%20analysis">Open</a> the tool in the user interface.

- Specify sequence(s) to analyze. This should be a _track_ item with custom or genomic sequences ([Input example](https://platform.genexplain.com/bioumlweb/#de=data%2FExamples%2FCombinatorial+regulation+analysis+of+TAL1%2FData%2FTAL1+track)). A _sequence source_ is suggested automatically.
- Select cell and tissue sources for filtering. There are over 400 cell types and more than 50 tissues to choose from. Please note that
multiple selection causes all models from the library to be considered that are associated with any one of the selected cells or tissues.
- Choose _Classification mode_ if _scan mode_ is not desired
- If _scan mode_, specify a step size and select _Best hit_ or _Cutoff_ mode
- If _Cutoff_ mode, specify a cutoff for model hits
- Specify a model accuracy cutoff
- Specify an output folder for results. The folder can already exist or be newly created by the workflow (<a href="https://platform.genexplain.com/bioumlweb/#de=data/Examples/Combinatorial%20regulation%20analysis%20of%20TAL1/Data/TAL1%20track%20(Combinatorial%20regulatory%20analysis)">Example result folder</a>).

<ol>
  <li>
    <a id="ref1">Katie Lloyd, Stamatia Papoutsopoulou, Emily Smith, Philip Stegmaier, Francois Bergey, et al., The SysmedIBD Consortium;
    Using systems medicine to identify a therapeutic agent with potential for repurposing in inflammatory bowel disease.</a>
    <a href="https://doi.org/10.1242/dmm.044040">Dis Model Mech 1 November 2020; 13 (11): dmm044040.</a>
  </li>
</ol>

