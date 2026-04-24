  
Fastq files (barcodes, forward and reverse) are on a directory named emp-paired-end-sequences.

Here I import them to qiime2  

```

qiime tools import \--type EMPPairedEndSequences \--input-path emp-paired-end-sequences \--output-path emp-paired-end-sequences.qza

```


Now I use the qza file generated and the barcode metadata to demultiplex the samples
  

```

qiime demux emp-paired \--i-seqs ../Raw/emp-paired-end-sequences.qza \--m-barcodes-file ../Metadata/q2_metadata_cbd_cbg.txt \--m-barcodes-column BarCodeSequence \--p-rev-comp-mapping-barcodes \--o-per-sample-sequences demux.qza \--o-error-correction-details demux-log.qza

```

demux vizualization

```

qiime demux summarize \--i-data demux.qza \--o-visualization demux.qzv

  

```