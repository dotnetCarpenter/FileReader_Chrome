
FileReader can be used to save PDF file to desk but Chrome needs `a.href = window.URL.createObjectURL(blob)` while iOS needs `a.href = reader.result`.


https://dotnetcarpenter.github.io/FileReader_Chrome/