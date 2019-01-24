
~~FileReader can be used to save PDF file to desk but Chrome needs `a.href = window.URL.createObjectURL(blob)` while iOS needs `a.href = reader.result`.~~

Turns out it was working with just FileReader all along.

## Known issues

1. Chrome has a hard limit of 25MB, if the PDF is larger than that, then the download is aborted.
2. Chrome also has an issue with UTF8 encoded PDF. Chrome can only convert ASCII encoding via the FileReader API, to base64 encoding. Firefox does the _right_ thing. IE11 and Edge uses a Microsoft API, that can handle UTF8.
3. iOS Safari (**not** desktop Safari) does not support the `download` attribute on a link, so you can not give the PDF a file name in iOS Safari.


https://dotnetcarpenter.github.io/FileReader_Chrome/

## To run locally

1. `npm i`
2. `npm start`
3. open web browser at `localhost:9000`
