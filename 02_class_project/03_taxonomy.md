1. Get taxonomy classifier
```
wget --no-check-certificate \-O 2024.09.backbone.v4.nb.qza \https://ftp.microbio.me/greengenes_release/2024.09/2024.09.backbone.v4.nb.qza
```

2. Run classification
```
qiime feature-classifier classify-sklearn \--i-reads ../dada2/seqs.qza \--i-classifier 2024.09.backbone.v4.nb.qza \--p-n-jobs 4 \--o-classification taxonomy_gg2.qza
```