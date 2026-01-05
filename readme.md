# Faiss
[[العربية]](readme.ar.md)

Alusus language bindings for the [FAISS library](https://github.com/facebookresearch/faiss) - A library for efficient similarity search and clustering of dense vectors.

## Overview

This library provides Alusus bindings to FAISS, enabling high-performance vector similarity search and clustering operations in the Alusus programming language.

## Installation

```alusus
import "Apm";
Apm.importFile("Alusus/Faiss");
use Faiss;
```

## Quick Start

```alusus
import "Srl/Console";
import "Srl/Array";
import "Apm";
Apm.importFile("Alusus/Faiss");
use Srl;
use Faiss;

// Create a flat index with 4-dimensional vectors
def index: ref[Index];
Index.new(index, 4, "Flat", MetricType.METRIC_INNER_PRODUCT);

// Add vectors to the index
def xb: Array[Float]({1.0, 2.0, 3.0, 4.0, 2.0, 3.0, 4.0, 5.0});
index.add(2, xb.buf);  // 2 vectors

// Search for nearest neighbors
def xq: Array[Float]({1.5, 2.5, 3.5, 4.5});
def labels: array[Int[64], 3];
def distances: array[Float, 3];
index.search(1, xq.buf, 3, distances, labels);  // Find 3 nearest neighbors

// Clean up
Index.free(index);
```

See complete examples in the `Examples/` directory.

## Documentation

This library wraps the FAISS C API. For detailed documentation of concepts, algorithms, and best practices, please refer to the official FAISS documentation:

- **Main Documentation**: https://github.com/facebookresearch/faiss/wiki
- **C API Reference**: https://github.com/facebookresearch/faiss/blob/main/c_api/
- **Getting Started Tutorial**: https://github.com/facebookresearch/faiss/wiki/Getting-started
- **Index Selection Guide**: https://github.com/facebookresearch/faiss/wiki/Guidelines-to-choose-an-index

## API Reference

### Core Classes

#### Index
Main index class for similarity search. [C API docs](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**Factory method:**
- `Index.new(obj: ref[ref[Index]], d: Int, description: CharsPtr, metric: Int): Int` - Create index using factory string

**Key methods:**
- `train(n: Int[64], x: ref[array[Float]]): Int` - Train the index on data
- `add(n: Int[64], x: ref[array[Float]]): Int` - Add vectors to index
- `search(n: Int[64], x: ref[array[Float]], k: Int[64], distances: ref[array[Float]], labels: ref[array[Int[64]]]): Int` - Search for k nearest neighbors
- `rangeSearch(n: Int[64], x: ref[array[Float]], radius: Float, result: ref[RangeSearchResult]): Int` - Range search
- `reset(): Int` - Remove all vectors from index
- `removeIds(sel: ref[IdSelector], nRemoved: ref[ArchWord]): Int` - Remove specific vectors

**Properties:**
- `d: Int[64]` - Vector dimension
- `nTotal: Int[64]` - Total number of indexed vectors
- `isTrained: Int` - Whether index is trained (0 or 1)
- `metricType: MetricType` - Distance metric being used
- `verbose: Int` - Verbosity level

**Cleanup:**
- `Index.free(obj: ref[Index])` - Free index memory

#### IndexFlat
Brute-force index performing exact search. [Guide](https://github.com/facebookresearch/faiss/wiki/Faiss-indexes#flat-indexes)

**Creation:**
- `IndexFlat.new(obj: ref[ref[IndexFlat]]): Int`
- `IndexFlat.new(obj: ref[ref[IndexFlat]], d: Int[64], metric: MetricType): Int`

**Additional methods:**
- `getXb(outXb: ref[ref[array[Float]]], outSize: ref[ArchWord])` - Get stored vectors
- `computeDistanceSubset(n: Int[64], x: ref[array[Float]], k: Int[64], outDistances: ref[array[Float]], labels: ref[array[Int[64]]]): Int` - Compute distances to subset

Inherits all Index methods.

#### IndexFlatIp
Flat index specialized for inner product metric. [Docs](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

**Creation:**
- `IndexFlatIp.new(obj: ref[ref[IndexFlatIp]]): Int`
- `IndexFlatIp.new(obj: ref[ref[IndexFlatIp]], d: Int[64]): Int`

#### IndexFlatL2
Flat index specialized for L2 (Euclidean) distance. [Docs](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

**Creation:**
- `IndexFlatL2.new(obj: ref[ref[IndexFlatL2]]): Int`
- `IndexFlatL2.new(obj: ref[ref[IndexFlatL2]], d: Int[64]): Int`

#### IndexIvf
Inverted file index for faster approximate search. [Guide](https://github.com/facebookresearch/faiss/wiki/Faiss-indexes#cell-probe-methods-indexivf-indexes)

**Additional properties:**
- `nList: ArchWord` - Number of inverted lists (clusters)
- `nProbe: ArchWord` - Number of clusters to visit during search (tunable)
- `quantizer: ref[Index]` - Quantizer index
- `ownFields: Int` - Whether index owns its fields

**Additional methods:**
- `mergeFrom(other: ref[IndexIvf], addId: Int[64]): Int` - Merge another IVF index
- `copySubsetTo(other: ref[IndexIvf], subsetType: Int, a1: Int[64], a2: Int[64]): Int` - Copy subset of vectors
- `getListSize(listNo: ArchWord): ArchWord` - Get size of inverted list
- `makeDirectMap(newMaintainDirectMap: Int): Int` - Create direct map for reconstruction
- `imbalanceFactor: Float[64]` - Get cluster imbalance factor
- `printStats()` - Print index statistics

#### IndexBinary
Index for binary (hamming) vectors. [Guide](https://github.com/facebookresearch/faiss/wiki/Binary-indexes)

Similar to Index but operates on binary vectors (Word[8] arrays instead of Float arrays).

### Support Classes

#### ParameterSpace
Manages index parameters for grid search and tuning. [C API](https://github.com/facebookresearch/faiss/blob/main/c_api/ParameterSpace_c.h)

**Methods:**
- `new(parameterSpace: ref[ref[ParameterSpace]]): Int`
- `setIndexParameter(index: ref[Index], paramName: CharsPtr, val: Float[64]): Int` - Set single parameter
- `setIndexParameters(index: ref[Index], params: CharsPtr): Int` - Set multiple parameters
- `addRange(name: CharsPtr, outRange: ref[ref[ParameterRange]]): Int` - Add parameter range

#### SearchParameters
Runtime search parameters. [C API](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**Methods:**
- `new(obj: ref[ref[SearchParameters]], sel: ref[IdSelector]): Int`
- `nProbe: Int` - Number of clusters to probe (for IVF indexes)

#### SearchParametersIvf
Extended search parameters for IVF indexes.

**Methods:**
- `new(obj: ref[ref[SearchParametersIvf]]): Int`
- `new(obj: ref[ref[SearchParametersIvf]], sel: ref[IdSelector], nprobe: ArchWord, maxCodes: ArchWord): Int`

**Properties:**
- `sel: ref[IdSelector]` - ID selector
- `nProbe: ArchWord` - Number of clusters to probe
- `maxCodes: ArchWord` - Maximum codes to scan

#### Clustering
K-means clustering implementation. [C API](https://github.com/facebookresearch/faiss/blob/main/c_api/Clustering_c.h)

**Creation:**
- `new(out: ref[ref[Clustering]], d: Int, k: Int): Int` - Create with dimension and k clusters
- `new(out: ref[ref[Clustering]], d: Int, k: Int, params: ptr[ClusteringParameters]): Int` - Create with parameters

**Methods:**
- `train(n: Int[64], x: ref[Float], index: ref[Index]): Int` - Run k-means
- `getCentroids(centroids: ref[ref[array[Float]]], size: ref[ArchWord])` - Get cluster centroids
- `getIterationStats(stats_out: ref[ref[ClusteringIterationStats]], size: ref[ArchWord])` - Get iteration statistics

**Properties:**
- `niter: Int` - Number of iterations
- `nredo: Int` - Number of k-means restarts
- `k: ArchWord` - Number of clusters
- `d: ArchWord` - Vector dimension

#### IdSelector
Select subsets of vectors by ID. [C API](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**Variants:**
- `IdSelectorBatch` - Select specific IDs from a list
- `IdSelectorRange` - Select IDs in a range
- `IdSelectorBitmap` - Select using a bitmap
- `IdSelectorNot` - Invert a selector
- `IdSelectorAnd` - Combine selectors with AND
- `IdSelectorOr` - Combine selectors with OR
- `IdSelectorXor` - Combine selectors with XOR

#### RangeSearchResult
Results from range search queries. [C API](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**Methods:**
- `new(obj: ref[ref[RangeSearchResult]], nq: Int[64]): Int`
- `doAllocation(): Int` - Allocate result buffers
- `bufferSize(): ArchWord` - Get buffer size
- `getLims(outLims: ref[ref[array[ArchWord]]])` - Get result limits array
- `getLabels(outLabels: ref[ref[array[Int[64]]]], outDistances: ref[ref[ref[Float]]])` - Get labels and distances

#### DistanceComputer
Compute distances to vectors. [C API](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**Methods:**
- `setQuery(x: ref[array[Float]]): Int` - Set query vector
- `vectorToQueryDis(i: Int[64], qd: ref[array[Float]]): Int` - Distance to query
- `symmetricDis(i: Int[64], j: Int[64], vd: ref[array[Float]]): Int` - Symmetric distance

### Constants

#### MetricType
Distance metrics. [Docs](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

- `METRIC_INNER_PRODUCT: 0` - Inner product (maximum similarity)
- `METRIC_L2: 1` - Euclidean distance (L2 norm)
- `METRIC_L1: 2` - Manhattan distance (L1 norm)
- `METRIC_LINF: 3` - Infinity norm (Chebyshev distance)
- `METRIC_LP: 4` - Lp norm
- `METRIC_CANBERRA: 20` - Canberra distance
- `METRIC_BRAY_CURTIS: 21` - Bray-Curtis dissimilarity
- `METRIC_JENSEN_SHANNON: 22` - Jensen-Shannon divergence

#### ErrorCode
Return codes from C API functions.

- `OK: 0` - Success
- `UNKNOWN_EXCEPT: -1` - Unknown exception
- `FAISS_EXCEPT: -2` - FAISS exception
- `STD_EXCEPT: -4` - Standard library exception

### Functions

- `getLastError(): CharsPtr` - Get last error message
- `kmeansClustering(d: ArchWord, n: ArchWord, k: ArchWord, x: ref[array[Float]], centroids: ref[array[Float]], q_error: ref[Float]) Int` - Standalone k-means

## GPU Support

To enable GPU acceleration, set the environment variable before running:
```bash
export FAISS_USE_GPU=1
```

The library will automatically load GPU-enabled binaries when available. See [FAISS GPU documentation](https://github.com/facebookresearch/faiss/wiki/Faiss-on-the-GPU) for details.

## Index Factory Strings

The `Index.new` factory method accepts strings to create different index types:

- `"Flat"` - Exact search (brute force)
- `"IVFn,Flat"` - IVF with n centroids, flat encoding
- `"IVFn,PQm"` - IVF with n centroids, PQ with m subquantizers
- `"HNSW32"` - Hierarchical navigable small world with 32 neighbors
- `"IVFn,HNSW32"` - Combined IVF and HNSW

See the [index factory documentation](https://github.com/facebookresearch/faiss/wiki/The-index-factory) for all available options and combinations.

## Examples

Complete working examples are in the `Examples/` directory:

- **example.alusus** - Basic flat index with inner product search
- **example2.alusus** - IVF index with parameter tuning

## Performance Tips

1. **Index Selection**:
   - Use `IndexFlat` for exact search on datasets <1M vectors
   - Use `IndexIVF` for approximate search on larger datasets
   - See the [index selection guide](https://github.com/facebookresearch/faiss/wiki/Guidelines-to-choose-an-index)

2. **Training**: IVF and other approximate indexes require training before adding vectors

3. **nprobe Parameter**: For IVF indexes, higher nprobe = better accuracy but slower search

4. **GPU Acceleration**: Enable GPU for operations on >10M vectors

5. **Memory**: Flat indexes store all vectors in memory; use compression for large datasets

See [FAISS performance guidelines](https://github.com/facebookresearch/faiss/wiki/Lower-memory-footprint) for detailed recommendations.

## Additional Resources

- **FAISS GitHub**: https://github.com/facebookresearch/faiss
- **FAISS Wiki**: https://github.com/facebookresearch/faiss/wiki
- **Research Paper**: [Billion-scale similarity search with GPUs](https://arxiv.org/abs/1702.08734)
- **Alusus Language**: https://alusus.org

## License

This binding follows the FAISS license (MIT). See the `license` file for details.
