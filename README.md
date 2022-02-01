# Trail of Bits public Semgrep rules

This repository contains Semgrep rules developed by Trail of Bits and made available to the public. They are part of our ongoing development efforts and are used in our security audits, vulnerability reseach, and internal projects. They will evolve over time as we identify new techniques.

## Using Semgrep

The easiest way to run the rules is to run them from the [Semgrep registry](https://semgrep.dev/p/trailofbits). To do so, navigate to the root folder of your project and run the following:

```shell
$ semgrep --config "p/trailofbits"
```

Alternatively, you can clone this repository, navigate to the root folder of your project, and run individual rules using the command below :

```shell
$ semgrep --config /path/to/semgrep-rules/semgreprule.yml
```

To run all rules from the cloned repository:

```shell
$ semgrep --config /path/to/semgrep-rules/ .
```

## Useful flags

Semgrep will run against all supported code files except for those in your `.gitignore` file. If you want to run the rules against all files and directories, including those in your `.gitignore`, add the `--no-git-ignore` flag.

```shell
$ semgrep --config /path/to/semgrep-rules/ . --no-git-ignore
```

You can also tell Semgrep to ignore files and directories that match any pattern. For instance, if you want to tell Semgrep to ignore all Go test files you can run the following:


```shell
$ semgrep --config /path/to/semgrep-rules/ . --exclude='*_test.go'
```

Use `-o` to output results to a file:

```shell
$ semgrep --config /path/to/semgrep-rules/hanging-goroutine.yml -o leaks.txt'
```

## Rules

Rule ID | Language | What it Finds
--- | --- | ---
[anonymous-race-condition](go/anonymous-race-condition.yml) | Go | Race conditions within anonymous goroutines
[hanging-goroutine](go/hanging-goroutine.yml) | Go | Goroutine leaks
[iterate-over-empty-collection](go/iterate-over-empty-collection.yml) | Go | Iterations over empty collection
[nil-check-after-call](go/nil-check-after-call.yml) | Go | Possible nil dereferences
[invalid-usage-of-modified-variable](go/invalid-usage-of-modified-variable.yml) | Go | Possible unintentional assignment when an error occurs
[servercodec-readrequestbody-unhandled-nil](go/servercodec-readrequestbody-unhandled-nil.yml) | Go | Possible incorrect `ServerCodec` interface implementation
[string-to-int-signedness-cast](go/string-to-int-signedness-cast.yml) | Go | Integer underflows
[sync-mutex-value-copied](go/sync-mutex-value-copied.yml) | Go | Copying of `sync.Mutex` via value receivers
[waitgroup-add-called-inside-goroutine](go/waitgroup-add-called-inside-goroutine.yml) | Go | Calls to `sync.WaitGroup.Add` inside of anonymous goroutines
[waitgroup-wait-inside-loop](go/waitgroup-wait-inside-loop.yml) | Go | Calls to `sync.WaitGroup.Wait` inside a loop
[racy-append-to-slice](go/racy-append-to-slice.yml) | Go | Concurrent calls to `append` from multiple goroutines
[racy-write-to-map](go/racy-write-to-map.yml) | Go | Concurrent writes to the same map in multiple goroutines
[missing-unlock-before-return](go/missing-unlock-before-return.yml) | Go | Missing mutex unlock before returning from a function. This could cause panics resulting from double lock operations
[missing-runlock-on-rwmutex](go/missing-runlock-on-rwmutex.yml) | Go | Missing RUnlock on an RWMutex lock before returning from a function.
[tarfile-extractall-traversal](python/tarfile-extractall-traversal.yml) | Python | Potential path traversal in call to `extractall` for a `tarfile`
[automatic-memory-pinning](python/automatic-memory-pinning.yml) | Python | Memory is not automatically pinned
[lxml-in-pandas](python/lxml-in-pandas.yml) | Python | Potential XXE attacks from loading lxml in pandas
[numpy-in-pytorch-modules](python/numpy-in-pytorch-modules.yml) | Python | Uses NumPy functions inside PyTorch modules 
[numpy-in-torch-datasets](python/numpy-in-torch-datasets.yml) | Python | Calls to the Numpy RNG inside of a Torch dataset
[pickles-in-numpy](python/pickles-in-numpy.yml) | Python | Potential arbitrary code execution from NumPy functions reliant on pickling
[pickles-in-pandas](python/pickles-in-pandas.yml) | Python | Potential arbitrary code execution from Pandas functions reliant on pickling
[pickles-in-pytorch](python/pickles-in-pytorch.yml) | Python | Potential arbitrary code execution from PyTorch functions reliant on pickling
[pickles-in-torch-distributed](python/pickles-in-torch-distributed.yml) | Python | Potential arbitrary code execution from PyTorch Distributed functions reliant on pickling
[torch-package](python/torch-package.yml) | Python | Potential arbitrary code execution from torch.package 
[torch-tensor](python/torch-tensor.yml) | Python | Possible parsing issues and inefficiency from improper tensor creation
[waiting-with-torch-distributed](python/waiting-with-torch-distributed.yml) | Python | Possible undefined behavior when not waiting for requests 
[panic-in-function-returning-result](rs/panic-in-function-returning-result.yml) | Rust | Calling `unwrap` or `expect` in a function returning a `Result`
