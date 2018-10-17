# R Notebook
Yikang Li  
2018-10-13  

# Data exploration of GloBi database  
  
Install and library package "rglobi":  

```r
library(rglobi)
```

```
## Warning: package 'rglobi' was built under R version 3.4.4
```


```r
library('dplyr')
```


## Scope of the database:  
The data from GloBi database are interaction data between species. Each row requires one source taxon, one target taxon and the interaction type that connects them.    

How many types of animals?  
?Can't achieve the entire dataset, still working on it.  

Variables in the database:   

```r
variables<- get_data_fields(opts = list())
variables
```

```
##                                               name
## 1                                         latitude
## 2                                        longitude
## 3                                         altitude
## 4                                     footprintWKT
## 5                                         locality
## 6                    collection_time_in_unix_epoch
## 7                                      study_title
## 8                                 interaction_type
## 9                                target_taxon_name
## 10                               source_taxon_name
## 11                       target_taxon_common_names
## 12                       source_taxon_common_names
## 13                        target_taxon_external_id
## 14                        source_taxon_external_id
## 15                               target_taxon_path
## 16                               source_taxon_path
## 17                         target_taxon_path_ranks
## 18                         source_taxon_path_ranks
## 19                           target_taxon_path_ids
## 20                           source_taxon_path_ids
## 21         target_specimen_frequency_of_occurrence
## 22 target_specimen_frequency_of_occurrence_percent
## 23                 target_specimen_total_volume_ml
## 24         target_specimen_total_volume_ml_percent
## 25                     target_specimen_total_count
## 26             target_specimen_total_count_percent
## 27               tmp_and_unique_target_specimen_id
## 28               tmp_and_unique_source_specimen_id
## 29             target_specimen_physiological_state
## 30          target_specimen_physiological_state_id
## 31             source_specimen_physiological_state
## 32          source_specimen_physiological_state_id
## 33                       target_specimen_body_part
## 34                    target_specimen_body_part_id
## 35                       source_specimen_body_part
## 36                    source_specimen_body_part_id
## 37                      source_specimen_life_stage
## 38                   source_specimen_life_stage_id
## 39                      target_specimen_life_stage
## 40                   target_specimen_life_stage_id
## 41                 source_specimen_basis_of_record
## 42                 target_specimen_basis_of_record
## 43                                      taxon_name
## 44                              taxon_common_names
## 45                               taxon_external_id
## 46                              taxon_external_url
## 47                                      taxon_path
## 48                                  taxon_path_ids
## 49                                taxon_path_ranks
## 50                                       study_url
## 51                                       study_doi
## 52                                  study_citation
## 53                           study_source_citation
## 54                                 study_source_id
## 55                         number_of_distinct_taxa
## 56                number_of_distinct_taxa_no_match
## 57                               number_of_sources
## 58                               number_of_studies
## 59                          number_of_interactions
## 60                                study_source_doi
## 61                             study_source_format
## 62                        study_source_archive_uri
## 63                       study_source_last_seen_at
##                                                                                   description
## 1                                                                   a description of latitude
## 2                                                                  a description of longitude
## 3                                                                   a description of altitude
## 4                                                               a description of footprintWKT
## 5                                                                   a description of locality
## 6                                              a description of collection_time_in_unix_epoch
## 7                                                                a description of study_title
## 8                                                           a description of interaction_type
## 9                                                          a description of target_taxon_name
## 10                                                         a description of source_taxon_name
## 11                                                 a description of target_taxon_common_names
## 12                                                 a description of source_taxon_common_names
## 13                                                  a description of target_taxon_external_id
## 14                                                  a description of source_taxon_external_id
## 15                                                         a description of target_taxon_path
## 16                                                         a description of source_taxon_path
## 17                                                   a description of target_taxon_path_ranks
## 18                                                   a description of source_taxon_path_ranks
## 19                                                     a description of target_taxon_path_ids
## 20                                                     a description of source_taxon_path_ids
## 21                                   a description of target_specimen_frequency_of_occurrence
## 22                           a description of target_specimen_frequency_of_occurrence_percent
## 23                                           a description of target_specimen_total_volume_ml
## 24                                   a description of target_specimen_total_volume_ml_percent
## 25                                               a description of target_specimen_total_count
## 26                                       a description of target_specimen_total_count_percent
## 27                                         a description of tmp_and_unique_target_specimen_id
## 28                                         a description of tmp_and_unique_source_specimen_id
## 29                                       a description of target_specimen_physiological_state
## 30                                    a description of target_specimen_physiological_state_id
## 31                                       a description of source_specimen_physiological_state
## 32                                    a description of source_specimen_physiological_state_id
## 33                                                 a description of target_specimen_body_part
## 34                                              a description of target_specimen_body_part_id
## 35                                                 a description of source_specimen_body_part
## 36                                              a description of source_specimen_body_part_id
## 37                                                a description of source_specimen_life_stage
## 38                                             a description of source_specimen_life_stage_id
## 39                                                a description of target_specimen_life_stage
## 40                                             a description of target_specimen_life_stage_id
## 41                                           a description of source_specimen_basis_of_record
## 42                                           a description of target_specimen_basis_of_record
## 43                                                                a description of taxon_name
## 44                                                        a description of taxon_common_names
## 45                                                         a description of taxon_external_id
## 46                                                        a description of taxon_external_url
## 47                                                                a description of taxon_path
## 48                                                            a description of taxon_path_ids
## 49                                                          a description of taxon_path_ranks
## 50                                                                 a description of study_url
## 51                                                                 a description of study_doi
## 52                                                            a description of study_citation
## 53                                                     a description of study_source_citation
## 54                                                           a description of study_source_id
## 55                                                      only available for /reports/* queries
## 56                                                      only available for /reports/* queries
## 57                                                      only available for /reports/* queries
## 58                                                      only available for /reports/* queries
## 59 available for /interaction queries by source/target taxon name and/or interactionType only
## 60                                                          a description of study_source_doi
## 61                                                       a description of study_source_format
## 62                                                  a description of study_source_archive_uri
## 63                                                 a description of study_source_last_seen_at
```


```r
length(variables[[1]])
```

```
## [1] 63
```
There are total of 63 variables in GloBi database.   

Interaction types:  

```r
get_interaction_types()
```

```
##           interaction     source     target
## 1                eats   consumer       food
## 2             eatenBy       food   consumer
## 3             preysOn   predator       prey
## 4        preyedUponBy       prey   predator
## 5               kills     killer     victim
## 6            killedBy     victim     killer
## 7          parasiteOf   parasite       host
## 8         hasParasite       host   parasite
## 9              hostOf       host   symbiont
## 10            hasHost   symbiont       host
## 11         pollinates pollinator      plant
## 12       pollinatedBy      plant pollinator
## 13         pathogenOf   pathogen       host
## 14        hasPathogen       host   pathogen
## 15           vectorOf     vector   pathogen
## 16          hasVector   pathogen     vector
## 17  dispersalVectorOf     vector       seed
## 18 hasDispersalVector       seed     vector
## 19         symbiontOf     source     target
## 20   flowersVisitedBy      plant    visitor
## 21    visitsFlowersOf    visitor      plant
## 22      interactsWith     source     target
##                                           termIRI
## 1       http://purl.obolibrary.org/obo/RO_0002470
## 2       http://purl.obolibrary.org/obo/RO_0002471
## 3       http://purl.obolibrary.org/obo/RO_0002439
## 4       http://purl.obolibrary.org/obo/RO_0002458
## 5       http://purl.obolibrary.org/obo/RO_0002626
## 6       http://purl.obolibrary.org/obo/RO_0002627
## 7       http://purl.obolibrary.org/obo/RO_0002444
## 8       http://purl.obolibrary.org/obo/RO_0002445
## 9       http://purl.obolibrary.org/obo/RO_0002453
## 10      http://purl.obolibrary.org/obo/RO_0002454
## 11      http://purl.obolibrary.org/obo/RO_0002455
## 12      http://purl.obolibrary.org/obo/RO_0002456
## 13      http://purl.obolibrary.org/obo/RO_0002556
## 14      http://purl.obolibrary.org/obo/RO_0002557
## 15      http://purl.obolibrary.org/obo/RO_0002459
## 16      http://purl.obolibrary.org/obo/RO_0002460
## 17    http://eol.org/schema/terms/DispersalVector
## 18 http://eol.org/schema/terms/HasDispersalVector
## 19      http://purl.obolibrary.org/obo/RO_0002440
## 20      http://purl.obolibrary.org/obo/RO_0002623
## 21      http://purl.obolibrary.org/obo/RO_0002622
## 22      http://purl.obolibrary.org/obo/RO_0002437
```


```r
length(get_interaction_types()[[1]])
```

```
## [1] 22
```
There are total of 22 types of interactions in this database.       

## Data Quality:  
Since later I will look at dataframe involving only interaction types "eats" and "eatenBy", let's analyze the quality of data with 'eats'.   

#### Completeness:  
Missing values:  

```r
data<- get_interactions_by_type(interactiontype = c("eats"))
head(data)
```

```
##   source_taxon_external_id source_taxon_name
## 1              WORMS:10194    Actinopterygii
## 2              WORMS:10194    Actinopterygii
## 3              WORMS:10194    Actinopterygii
## 4              WORMS:10194    Actinopterygii
## 5              WORMS:10194    Actinopterygii
## 6              WORMS:10194    Actinopterygii
##                                                                    source_taxon_path
## 1 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 2 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 3 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 4 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 5 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 6 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
##   source_specimen_life_stage interaction_type target_taxon_external_id
## 1                         NA             eats                 no:match
## 2                         NA             eats                 no:match
## 3                         NA             eats                 no:match
## 4                         NA             eats                 no:match
## 5                         NA             eats                 no:match
## 6                         NA             eats                 no:match
##                target_taxon_name target_taxon_path
## 1                        benthos                  
## 2 micro-benthos and meio-benthos                  
## 3             benthic autotrophs                  
## 4           marine invertebrates                  
## 5             benthic herbivores                  
## 6    detritivorous invertebrates                  
##   target_specimen_life_stage latitude longitude study_citation
## 1                         NA       NA        NA             NA
## 2                         NA       NA        NA             NA
## 3                         NA       NA        NA             NA
## 4                         NA       NA        NA             NA
## 5                         NA       NA        NA             NA
## 6                         NA       NA        NA             NA
##   study_source_citation
## 1                    NA
## 2                    NA
## 3                    NA
## 4                    NA
## 5                    NA
## 6                    NA
```

```r
apply(is.na(data), 2, sum)
```

```
##   source_taxon_external_id          source_taxon_name 
##                          0                          0 
##          source_taxon_path source_specimen_life_stage 
##                          0                       1024 
##           interaction_type   target_taxon_external_id 
##                          0                          0 
##          target_taxon_name          target_taxon_path 
##                          0                          0 
## target_specimen_life_stage                   latitude 
##                       1024                       1024 
##                  longitude             study_citation 
##                       1024                       1024 
##      study_source_citation 
##                       1024
```
Above all, we can see variables "source_specimen_life_stage", "target_specimen_life_stage", "latitude
", "longitude", "study_citation", "study_source_citation" are missing. Missing "latitude" and "longitude" means missing location data, which should be considered as an issue if we want to do visualizations on the map.  

Except that, there are other missing values like "no:match" in column "target_taxon_external_id" and "no name" in column "target_taxon_name":   

```r
head(data%>%
  filter(target_taxon_external_id == 'no:match'))
```

```
##   source_taxon_external_id source_taxon_name
## 1              WORMS:10194    Actinopterygii
## 2              WORMS:10194    Actinopterygii
## 3              WORMS:10194    Actinopterygii
## 4              WORMS:10194    Actinopterygii
## 5              WORMS:10194    Actinopterygii
## 6              WORMS:10194    Actinopterygii
##                                                                    source_taxon_path
## 1 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 2 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 3 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 4 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 5 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 6 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
##   source_specimen_life_stage interaction_type target_taxon_external_id
## 1                         NA             eats                 no:match
## 2                         NA             eats                 no:match
## 3                         NA             eats                 no:match
## 4                         NA             eats                 no:match
## 5                         NA             eats                 no:match
## 6                         NA             eats                 no:match
##                target_taxon_name target_taxon_path
## 1                        benthos                  
## 2 micro-benthos and meio-benthos                  
## 3             benthic autotrophs                  
## 4           marine invertebrates                  
## 5             benthic herbivores                  
## 6    detritivorous invertebrates                  
##   target_specimen_life_stage latitude longitude study_citation
## 1                         NA       NA        NA             NA
## 2                         NA       NA        NA             NA
## 3                         NA       NA        NA             NA
## 4                         NA       NA        NA             NA
## 5                         NA       NA        NA             NA
## 6                         NA       NA        NA             NA
##   study_source_citation
## 1                    NA
## 2                    NA
## 3                    NA
## 4                    NA
## 5                    NA
## 6                    NA
```
    

```r
data%>%
  filter(target_taxon_name == 'no name')
```

```
##   source_taxon_external_id source_taxon_name
## 1              WORMS:10194    Actinopterygii
##                                                                    source_taxon_path
## 1 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
##   source_specimen_life_stage interaction_type target_taxon_external_id
## 1                         NA             eats                 no:match
##   target_taxon_name target_taxon_path target_specimen_life_stage latitude
## 1           no name                                           NA       NA
##   longitude study_citation study_source_citation
## 1        NA             NA                    NA
```
   
#### Consistency and Accuracy:  
Several problems are found when I was looking at the data with interaction type "eats":    

1. The specific levels of "taxon_path" are inconsistent. 
For example, the first two unique taxon_paths in "data" are:   
"Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii" (Biota | Kingdom | Phylum | Subphylum | Infraphylum | ? | Class)  
& "Aves | Ciconiiformes | Laridae | Larus | Larus argentatusLarus" (Class | Order | Family | Genus | species)

Out of these two paths, one of them is specific from biota to class, the other is from class to species, which causes inconsistency in format.   

2. Problems with accuracy:   
For example, the value for "source_taxon_path" in the first row is like:  

```r
data[1,]$source_taxon_path
```

```
## [1] "Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii"
```
However, according to Wikipedia, it should be "Osteichthyes" instead of "Pisces". Actinopterygii (ray finned fishes) is a Subclass of Class Osteichthyes (bony fish).   

3. There are also some weird records:  

```r
data%>%
  filter(source_taxon_external_id == target_taxon_external_id)
```

```
##   source_taxon_external_id source_taxon_name
## 1              WORMS:10194    Actinopterygii
## 2              WORMS:10194    Actinopterygii
##                                                                    source_taxon_path
## 1 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 2 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
##   source_specimen_life_stage interaction_type target_taxon_external_id
## 1                         NA             eats              WORMS:10194
## 2                         NA             eats              WORMS:10194
##   target_taxon_name
## 1    Actinopterygii
## 2    Actinopterygii
##                                                                    target_taxon_path
## 1 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 2 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
##   target_specimen_life_stage latitude longitude study_citation
## 1                         NA       NA        NA             NA
## 2                         NA       NA        NA             NA
##   study_source_citation
## 1                    NA
## 2                    NA
```
In the above 2 rows, the source_taxon and target_taxon are the same: "Actinopterygii", which means Actinopterygii eats itself. It is true that some species cannibalise each other, but I haven't found such actions among Actinopterygii.   
 

#### Uniqueness:  
No. The entities within the dataset are not unique. This can be known by testing the length before and after removing duplicated rows:    

```r
length(data[[1]])
```

```
## [1] 1024
```

```r
length(data[!duplicated(data),][[1]])
```

```
## [1] 616
```

#### Conformity:  
So far, I believe that the data conform to the right conventions and standards.  


#### Standards that are required to input data into GloBi (cited from https://www.globalbioticinteractions.org/contribute)  
"Provide a (permanent) url to a web-accessible existing interaction dataset along with a data citation. Any structured data format / API will do, and csv/tsv file formats are preferred. Examples includes references to openly accessible datapaper (e.g. Raymond et al. 2011, Ferrer-Paris et al. 2014), data hosted in github (e.g. Hurlbert 2014) or publicly accessible APIs (e.g. iNaturalist). For citations, DOIs are preferred, but any will do as long as they describe the source of the data."   

## Explore the data:  
I am particularly interested in interaction types 'eats' and 'eatenBy'. It will be awesome to recognize some interesting patterns using GloBi database. For example, do species from same genus or family (or with similar taxon path) eat similar species? (Cause some difficulty because of the inconsistency in format of path)  
I am also thinking about making visualizations of the global biotic food chain.    
While without the data of lat and lon (location), we have to narrow our scope of study.   


For example, explore "eats" and "eatenBy" interaction data for source_taxon: 'Actinopterygii', we can see there are 216 unique species that are eaten by Actinopterygii:  

```r
data10194<- get_interactions_by_type(interactiontype = c("eats"))%>%
  filter(source_taxon_external_id == 'WORMS:10194')
head(data10194)
```

```
##   source_taxon_external_id source_taxon_name
## 1              WORMS:10194    Actinopterygii
## 2              WORMS:10194    Actinopterygii
## 3              WORMS:10194    Actinopterygii
## 4              WORMS:10194    Actinopterygii
## 5              WORMS:10194    Actinopterygii
## 6              WORMS:10194    Actinopterygii
##                                                                    source_taxon_path
## 1 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 2 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 3 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 4 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 5 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
## 6 Biota | Animalia | Chordata | Vertebrata | Gnathostomata | Pisces | Actinopterygii
##   source_specimen_life_stage interaction_type target_taxon_external_id
## 1                         NA             eats                 no:match
## 2                         NA             eats                 no:match
## 3                         NA             eats                 no:match
## 4                         NA             eats                 no:match
## 5                         NA             eats                 no:match
## 6                         NA             eats                 no:match
##                target_taxon_name target_taxon_path
## 1                        benthos                  
## 2 micro-benthos and meio-benthos                  
## 3             benthic autotrophs                  
## 4           marine invertebrates                  
## 5             benthic herbivores                  
## 6    detritivorous invertebrates                  
##   target_specimen_life_stage latitude longitude study_citation
## 1                         NA       NA        NA             NA
## 2                         NA       NA        NA             NA
## 3                         NA       NA        NA             NA
## 4                         NA       NA        NA             NA
## 5                         NA       NA        NA             NA
## 6                         NA       NA        NA             NA
##   study_source_citation
## 1                    NA
## 2                    NA
## 3                    NA
## 4                    NA
## 5                    NA
## 6                    NA
```


```r
head(unique(data10194['target_taxon_name']))
```

```
##                target_taxon_name
## 1                        benthos
## 2 micro-benthos and meio-benthos
## 3             benthic autotrophs
## 4           marine invertebrates
## 5             benthic herbivores
## 6    detritivorous invertebrates
```
What are the similaries or difference between these target taxon?   
Fields to study: Path, physiological_state, frequency_of_occurrence(percent), total_volume_ml, total_volume_ml_percent, total_count, total_count_percent.  

## Issues:  
No function provided to achieve all records.   
Only 1000 records are shown when trying to extract data.   

```r
unique(get_interactions_by_type(interactiontype = c("eats"))['source_taxon_name'])
```

```
##            source_taxon_name
## 1             Actinopterygii
## 438         Larus argentatus
## 602           Ardea herodias
## 798            Larus marinus
## 818 Haliaeetus leucocephalus
```
Could only get data for 5 unique source taxon.  


Functionsdon't work, fields are not shown, could only show default fields: c("source_taxon_external_id","source_taxon_name", "source_taxon_path", "source_specimen_life_stage", "interaction_type", "target_taxon_external_id", "target_taxon_name", "target_taxon_path", "target_specimen_life_stage", "latitude", "longitude", "study_citation", "study_external_id", "study_source_citation")?

```r
head(get_interactions_by_taxa('Larus marinus', interactiontype = 'eats', showfield = c('target_specimen_frequency_of_occurrence',	
'target_specimen_frequency_of_occurrence_percent',	
'target_specimen_total_volume_ml')))
```

```
##   source_taxon_external_id source_taxon_name
## 1              EOL:1049577     Larus marinus
## 2              EOL:1049577     Larus marinus
## 3              EOL:1049577     Larus marinus
## 4              EOL:1049577     Larus marinus
## 5              EOL:1049577     Larus marinus
## 6              EOL:1049577     Larus marinus
##                                                                source_taxon_path
## 1 Animalia | Chordata | Aves | Charadriiformes | Laridae | Larus | Larus marinus
## 2 Animalia | Chordata | Aves | Charadriiformes | Laridae | Larus | Larus marinus
## 3 Animalia | Chordata | Aves | Charadriiformes | Laridae | Larus | Larus marinus
## 4 Animalia | Chordata | Aves | Charadriiformes | Laridae | Larus | Larus marinus
## 5 Animalia | Chordata | Aves | Charadriiformes | Laridae | Larus | Larus marinus
## 6 Animalia | Chordata | Aves | Charadriiformes | Laridae | Larus | Larus marinus
##   source_specimen_life_stage source_specimen_basis_of_record
## 1                         NA                              NA
## 2                         NA                              NA
## 3                         NA                              NA
## 4                         NA                              NA
## 5                         NA                              NA
## 6                         NA                              NA
##   interaction_type target_taxon_external_id    target_taxon_name
## 1             eats                 no:match               Others
## 2             eats                 no:match               others
## 3             eats               EOL:206899 Ammodytes americanus
## 4             eats              EOL:2773054        Gnathostomata
## 5             eats               EOL:206050 Trisopterus esmarkii
## 6             eats     FBC:FB:SpecCode:3822 Ammodytes hexapterus
##                                                                                              target_taxon_path
## 1                                                                                                             
## 2                                                                                                             
## 3          Animalia | Chordata | Actinopterygii | Perciformes | Ammodytidae | Ammodytes | Ammodytes americanus
## 4 Animalia | Bilateria | Deuterostomia | Echinodermata | Echinozoa | Echinoidea | Euechinoidea | Gnathostomata
## 5             Animalia | Chordata | Actinopterygii | Gadiformes | Gadidae | Trisopterus | Trisopterus esmarkii
## 6                                Actinopterygii | Perciformes | Ammodytidae | Ammodytes | Ammodytes hexapterus
##   target_specimen_life_stage target_specimen_basis_of_record latitude
## 1                         NA                              NA       NA
## 2                         NA                              NA       NA
## 3                         NA                              NA       NA
## 4                         NA                              NA       NA
## 5                         NA                              NA       NA
## 6                         NA                              NA       NA
##   longitude study_title
## 1        NA          NA
## 2        NA          NA
## 3        NA          NA
## 4        NA          NA
## 5        NA          NA
## 6        NA          NA
```

