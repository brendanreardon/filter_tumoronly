# Common variant filter
A simple filter to annotate and filter somatic variants based on their occurence in [ExAC](http://exac.broadinstitute.org/). This is the same filter applied in [VCF2MAF's common variant filter](https://github.com/mskcc/vcf2maf/blob/master/docs/vep_maf_readme.txt), as used by [AACR Project GENIE](http://cancerdiscovery.aacrjournals.org/content/7/8/818). A variant is filtered if at least 10 alleles containing that variant are present across any subpopulation in ExAC, unless it appears at a [known somatic site](https://github.com/mskcc/vcf2maf/blob/v1.6.12/data/known_somatic_sites.bed). 

This filter was originally implemented by [Cyriac Kandoth](https://github.com/ckandoth) for [VCF2MAF](https://github.com/mskcc/vcf2maf). 

## Getting common_variant_filter
This codebase is available for download through this Github repository and [Dockerhub](https://hub.docker.com/r/vanallenlab/common_variant_filter/).

To download via Github
```
git clone https://github.com/vanallenlab/common_variant_filter
```

To download via Dockerhub
```
docker pull vanallenlab/common_variant_filter:1.0.4
```

## Using common_variant_filter
common_variant_filter accepts the following arguments
- `id`: Sample ID
- `maf`: A path to a MAF file containing somatic variants for annotation and filtration
- `min_exac_ac`: (Optional) Default `10`, minimum allele count across any ExAC population to filter
- `min_filter_depth`: (Optional) Default `0`, minimum coverage of variant to not be filtered
- `filter_noncoding`: (Optional) Default `False`, filters non-coding variants
- `disable_known_sites`: (Optional) Default `False`, will disable keeping variants that appear at known somatic sites, regardless of allele counts in ExAC
- `disable_wl`: (Optional) Default `False`, equivalent to `--disable_known_sites` and will be deprecated in future release
- `hashtagged_header`: (Optional) Default `False`, will read into pandas with `comment="#"` to remove MAF header

An example run command would be the following,

`python /common_variant_filter.py --id $sampleId --maf $maf --min_exac_ac 10 --min_filter_depth 0 --filter_noncoding --disable_known_sites --hashtagged_header`

## References
1. [Lek M, Karczewski KJ, Minikel EV, et al. Analysis of protein-coding genetic variation in 60,706 humans. Nature. 2016;536(7616):285-91.](https://www.nature.com/articles/nature19057)
2. [AACR Project GENIE: Powering Precision Medicine through an International Consortium. Cancer Discov. 2017;7(8):818-831.](http://cancerdiscovery.aacrjournals.org/content/7/8/818)
