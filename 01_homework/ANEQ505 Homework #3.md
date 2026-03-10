~={red}(1point)=~ for Alpha Rarefaction Plot
Run Core Metrics ~={red}(1 point; .25pts per line)=~
Make alpha diversity plots ~={red}(3points)=~
~={red}10 points=~ for the questions 

~={red}15 points total=~
------------------------------------------------------------------

Due: 

**For complete credit for this assignment, you must answer all questions and include all commands in your obsidian upload.**

------------------------------------------------------------------
**Learning Objectives**
1. Practice recording commands and editing code to match your analysis.
2. Perform alpha rarefaction and determine an appropriate sequencing depth.
3. Run core metrics, generate plots for alpha and beta diversity
--------------------------------------------------

**Cow Site Data Workflow**, part 3

Load qiime2 in a terminal session after you go into the **cow** folder

```
module purge

module load qiime2/2024.10_amplicon

```

### Alpha Rarefaction Plot ~={red}(1 point)=~
- Chose the input sequencings depths (min and max) for generating the alpha rarefaction plot: 

```
#go to the cow directory

qiime diversity alpha-rarefaction \--i-table dada2/cow_table_dada2_filtered300.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization alpha_rarefaction_curves_16S.qzv \--p-min-depth 1 \--p-max-depth 6000
```


### Run Core Metrics ~={red}(1 point)=~

```
qiime diversity core-metrics-phylogenetic \--i-table dada2/cow_table_dada2_filtered300.qza \--i-phylogeny tree/tree_gg2.qza \--m-metadata-file metadata/cow_metadata.txt \--p-sampling-depth 2500 \--output-dir core_metrics_results
```


### Visualize alpha diversity plots
- generate a plot to visualize the observed features ~={red}(1 point)=~
```
qiime diversity alpha-group-significance \--i-alpha-diversity core_metrics_results/observed_features_vector.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization core_metrics_results/observed_features_vector.qzv
```

- generate a plot to visualize faith's PD ~={red}(2 points)=~
```
qiime diversity alpha-group-significance \--i-alpha-diversity core_metrics_results/faith_pd_vector.qza \--m-metadata-file metadata/cow_metadata.txt \--o-visualization core_metrics_results/faith_pd_vector.qzv

```



## Homework questions ~={red}(10 points)=~

1. what is the name of the file you needed to use to figure out what min and max depths to use to generate the alpha rarefaction plot? (Hint: which file contains the sequencing depths for each sample)

cow_table_dada2_filtered300.qzv

2. what did you choose for the rarefaction depth (the input for core metrics -p-sampling-depth flag)? why? 

2500 because I wanted to keet the most observations possible per sample without loosing samples and becasue at this point the shannon index was at a plateau already

3. Which cow body location had more observed features? Which has the lowest?

in average it seems that fecal samples have more features observed, although skin have more variability and seems to have some samples with more observed features.

nassal samples have the less features observed.

4. What is the main difference between Faiths PD and Shannons alpha diversity metrics?  

Faith take into consideration the phylogeny while Shannons does not.

5. Which diversity metrics produced by the core-metrics pipeline require phylogenetic information?

Faith diversity, and weighted and unweighted unifrac

6. Which two body sites have the highest Faiths PD alpha diversity?  Are the groups significantly different?

Skin have more Faiths diversity and yes, the groups are significantly different.

7. Does it seem like there are any groupings in the beta diversity? What are the groupings? 

There are three main gorups, fecal, nasal-oral and skin-udder

8. Why do you think these samples are grouping together? 

They are grouping because they are similar to other samples on the same site or a similar/closer site (for example nose is close to mouth and skin and udder share a spatial continuity) and are different from sample on different sites.

9. What test can you run to determine if the groups are significantly different?

A PERMANOVA since the samples are independent

10. What command would you use to run that test?

```
qiime diversity beta-group-significance \--i-distance-matrix core-metrics-results/unweighted_unifrac_distance_matrix.qza \--m-metadata-file metadata/cow_metadata.txt \--m-metadata-column body_site \--o-visualization core-metrics-results/unweighted_unifrac_distance_matrix.qzv


```