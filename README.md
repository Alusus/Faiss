# Alusus FAISS Bindings

**FAISS upstream README:** `https://github.com/facebookresearch/faiss/blob/main/README.md`

This document lists the most important Alusus‐level functions and their corresponding FAISS C API calls.

| Alusus Function                                     | C API Function                                    |
|-----------------------------------------------------|---------------------------------------------------|
| **Factory & Creation**                              |                                                   |
| `faissIndexFactory`                                 | `faiss_index_factory`                             |
| `faissIndexBinaryFactory`                           | `faiss_index_binary_factory`                      |
| `faissIndexFlatNew`                                 | `faiss_IndexFlat_new`                             |
| `faissIndexFlatNewWith`                             | `faiss_IndexFlat_new_with`                        |
| `faissIndexFlatIPNew`                               | `faiss_IndexFlatIP_new`                           |
| `faissIndexFlatL2New`                               | `faiss_IndexFlatL2_new`                           |
| `faissIndexRefineFlatNew`                           | `faiss_IndexRefineFlat_new`                       |
| `faissIndexFlat1DNew`                               | `faiss_IndexFlat1D_new`                           |
| `faissSearchParametersIVFNew`                       | `faiss_SearchParametersIVF_new`                   |
| `faissSearchParametersIVFNewWith`                   | `faiss_SearchParametersIVF_new_with`              |
| `faissIndexIVFFlatNew`                              | `faiss_IndexIVF_new`                              |
| `faissIndexBinaryIVFNew`                            | `faiss_IndexBinaryIVF_new`                        |

| **Configuration & Training**                        |                                                   |
| `faissSearchParametersIVFSetNprobe`                 | `faiss_SearchParameters_set_nprobe`               |
| `faissSearchParametersIVFSetMaxCodes`               | `faiss_SearchParameters_set_max_codes`            |
| `faissIndexRefineFlatSetOwnFields`                  | `faiss_IndexRefineFlat_set_own_fields`            |
| `faissIndexRefineFlatSetKFactor`                    | `faiss_IndexRefineFlat_set_k_factor`              |
| `faissParameterSpaceSetIndexParameters`             | `faiss_ParameterSpace_set_index_parameters`       |
| `faissIndexTrain`                                   | `faiss_Index_train`                               |
| `faissIndexIVFTrainEncoder`                         | `faiss_IndexIVF_train_encoder`                    |

| **Data Ingestion & Manipulation**                   |                                                   |
| `faissIndexAdd`                                     | `faiss_Index_add`                                 |
| `faissIndexAddWithIds`                              | `faiss_Index_add_with_ids`                        |
| `faissIndexReset`                                   | `faiss_Index_reset`                               |
| `faissIndexRemoveIds`                               | `faiss_Index_remove_ids`                          |
| `faissIndexRangeSearch`                             | `faiss_Index_range_search`                        |
| `faissBufferListAdd`                                | `faiss_BufferList_add`                            |
| `faissRangeSearchResultDoAllocation`                | `faiss_RangeSearchResult_do_allocation`           |

| **Query & Search**                                  |                                                   |
| `faissIndexSearch`                                  | `faiss_Index_search`                              |
| `faissIndexSearchWithParams`                        | `faiss_Index_search_with_params`                  |
| `faissIndexRangeSearch`                             | `faiss_Index_range_search`                        |
| `faissIndexIVFSearchPreassigned`                    | `faiss_IndexIVF_search_preassigned`               |
| `faissIndexBinaryIVFSearchPreassigned`              | `faiss_IndexBinaryIVF_search_preassigned`         |
| `faissDistanceComputerSetQuery`                     | `faiss_DistanceComputer_set_query`                |
| `faissDistanceComputerVectorToQueryDis`             | `faiss_DistanceComputer_vector_to_query_dis`      |
| `faissDistanceComputerSymmetricDis`                 | `faiss_DistanceComputer_symmetric_dis`            |

| **Inspection & Statistics**                         |                                                   |
| `faissIndexFlatXb`                                  | `faiss_IndexFlat_xb`                              |
| `faissIndexIVFGetListSize`                          | `faiss_IndexIVF_get_list_size`                    |
| `faissIndexBinaryIVFGetListSize`                    | `faiss_IndexBinaryIVF_get_list_size`              |
| `faissIndexIVFMakeDirectMap`                        | `faiss_IndexIVF_make_direct_map`                  |
| `faissIndexBinaryIVFMakeDirectMap`                  | `faiss_IndexBinaryIVF_make_direct_map`            |
| `faissIndexIVFImbalanceFactor`                      | `faiss_IndexIVF_imbalance_factor`                 |
| `faissIndexBinaryIVFImbalanceFactor`                | `faiss_IndexBinaryIVF_imbalance_factor`           |
| `faissIndexIVFPrintStats`                           | `faiss_IndexIVF_print_stats`                      |
| `faissIndexBinaryIVFPrintStats`                     | `faiss_IndexBinaryIVF_print_stats`                |
| `faissGetIndexIVFStats`                             | `faiss_get_indexIVF_stats`                        |

| **Destruction**                                     |                                                   |
| `faissIndexFlatFree`                                | `faiss_IndexFlat_free`                            |
| `faissIndexFlatIPFree`                              | `faiss_IndexFlatIP_free`                          |
| `faissIndexFlatL2Free`                              | `faiss_IndexFlatL2_free`                          |
| `faissIndexRefineFlatFree`                          | `faiss_IndexRefineFlat_free`                      |
| `faissIndexFlat1DFree`                              | `faiss_IndexFlat1D_free`                          |
| `faissIndexIVFFlatFree`                             | `faiss_IndexIVF_free`                             |
| `faissIndexBinaryIVFFree`                           | `faiss_IndexBinaryIVF_free`                       |
| `faissIndexFree`                                    | `faiss_Index_free`                                |
| `faissSearchParametersIVFFree`                      | `faiss_SearchParameters_free`                     |
| `faissRangeSearchResultFree`                        | `faiss_RangeSearchResult_free`                    |
| `faissBufferListFree`                               | `faiss_BufferList_free`                           |
| `faissDistanceComputerFree`                         | `faiss_DistanceComputer_free`                     |


