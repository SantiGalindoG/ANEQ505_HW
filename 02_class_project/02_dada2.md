```
qiime dada2 denoise-paired \--i-demultiplexed-seqs ../demux/demux.qza \--p-trunc-len-f 250 \--p-trunc-len-r 225 \--p-n-threads 4 \--o-table table.qza \--o-representative-sequences seqs.qza \--o-denoising-stats dada2_stats.qza

```