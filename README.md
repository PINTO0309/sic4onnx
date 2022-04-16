# sic4onnx
A very simple tool that forces a change in the IR Version of an ONNX graph. **S**imple **I**R version **C**hanger for **ONNX**.


https://github.com/PINTO0309/simple-onnx-processing-tools

[![Downloads](https://static.pepy.tech/personalized-badge/sic4onnx?period=total&units=none&left_color=grey&right_color=brightgreen&left_text=Downloads)](https://pepy.tech/project/sic4onnx) ![GitHub](https://img.shields.io/github/license/PINTO0309/sic4onnx?color=2BAF2B) [![PyPI](https://img.shields.io/pypi/v/sic4onnx?color=2BAF2B)](https://pypi.org/project/sic4onnx/) [![CodeQL](https://github.com/PINTO0309/sic4onnx/workflows/CodeQL/badge.svg)](https://github.com/PINTO0309/sic4onnx/actions?query=workflow%3ACodeQL)

## 1. Setup
### 1-1. HostPC
```bash
### option
$ echo export PATH="~/.local/bin:$PATH" >> ~/.bashrc \
&& source ~/.bashrc

### run
$ pip install -U onnx \
&& pip install -U sic4onnx
```
### 1-2. Docker
```bash
### docker pull
$ docker pull pinto0309/sic4onnx:latest

### docker build
$ docker build -t pinto0309/sic4onnx:latest .

### docker run
$ docker run --rm -it -v `pwd`:/workdir pinto0309/sic4onnx:latest
$ cd /workdir
```

## 2. CLI Usage
```bash
$ sic4onnx -h

usage:
    sic4onnx [-h]
    --input_onnx_file_path INPUT_ONNX_FILE_PATH
    --output_onnx_file_path OUTPUT_ONNX_FILE_PATH
    --ir_version IR_VERSION
    [--non_verbose]

optional arguments:
  -h, --help
        show this help message and exit

  --input_onnx_file_path INPUT_ONNX_FILE_PATH
        Input onnx file path.

  --output_onnx_file_path OUTPUT_ONNX_FILE_PATH
        Output onnx file path.

  --ir_version OPSET
        IR version number to be changed. e.g. --ir_version 8

  --non_verbose
        Do not show all information logs. Only error logs are displayed.
```

## 3. In-script Usage
```python
$ python
>>> from sic4onnx import irchange
>>> help(irchange)
Help on function change in module sic4onnx.onnx_irversion_change:

change(
  ir_version: int,
  input_onnx_file_path: Union[str, NoneType] = '',
  output_onnx_file_path: Union[str, NoneType] = '',
  onnx_graph: Union[onnx.onnx_ml_pb2.ModelProto, NoneType] = None,
  non_verbose: Union[bool, NoneType] = False
) -> onnx.onnx_ml_pb2.ModelProto

    Parameters
    ----------
    ir_version: int
        IR version number to be changed.
        e.g. --ir_version 8

    input_onnx_file_path: Optional[str]
        Input onnx file path.
        Either input_onnx_file_path or onnx_graph must be specified.

    output_onnx_file_path: Optional[str]
        Output onnx file path.
        If output_onnx_file_path is not specified, no .onnx file is output.

    onnx_graph: Optional[onnx.ModelProto]
        onnx.ModelProto.
        Either input_onnx_file_path or onnx_graph must be specified.
        onnx_graph If specified, ignore input_onnx_file_path and process onnx_graph.

    non_verbose: Optional[bool]
        Do not show all information logs. Only error logs are displayed.
        Default: False

    Returns
    -------
    ir_changed_graph: onnx.ModelProto
        IR version changed onnx ModelProto
```

## 4. CLI Execution
```bash
$ sic4onnx \
--input_onnx_file_path input.onnx \
--output_onnx_file_path output.onnx \
--ir_version 8
```

## 5. In-script Execution
```python
from sic4onnx import irchange

changed_graph = change(
    onnx_graph=graph,
    ir_version=8,
    non_verbose=True,
)
```
