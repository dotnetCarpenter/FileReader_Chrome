
~~FileReader can be used to save PDF file to desk but Chrome needs `a.href = window.URL.createObjectURL(blob)` while iOS needs `a.href = reader.result`.~~

Turns out it was working with just FileReader all along. But Chrome is suspect to port forwarding errors when
downloading...


https://dotnetcarpenter.github.io/FileReader_Chrome/

## To run locally

1. `npm i`
2. `npm start`
3. open web browser at `localhost:9000`
