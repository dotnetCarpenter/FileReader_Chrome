
~~FileReader can be used to save PDF file to desk but Chrome needs `a.href = window.URL.createObjectURL(blob)` while iOS needs `a.href = reader.result`.~~

Turns out it was working with just FileReader all along.

## Known issues

1. Chrome has a hard limit of 25MB, if the PDF is larger than that, then the download is aborted.
2. Chrome also has an issue with UTF8 encoded PDF. Chrome can only convert ASCII encoding via the FileReader API, to base64 encoding. Firefox does the _right_ thing. IE11 and Edge uses a Microsoft API, that can handle UTF8.
3. iOS Safari (**not** desktop Safari) does not support the `download` attribute on a link, so you can not give the PDF a file name in iOS Safari. https://bugs.webkit.org/show_bug.cgi?id=167341

https://dotnetcarpenter.github.io/FileReader_Chrome/

## To run locally

1. `npm i`
2. `npm start`
3. open web browser at `localhost:9000`


# Chrome bug report

## FileReader readAsDataURL can not base64 encode utf-8 characters in a PDF file

https://bugs.chromium.org/p/chromium/issues/detail?id=925096

**Steps to reproduce the problem:**

1. Download all attached files
2. Run index.html in a local web server
3. Make sure that "utf8.pdf" is checked
4. Click on "Save PDF" button

**Does this feature work correctly in other browsers?**

Yes - This is just a Chromium problem

**What is the expected behavior?**

Chrome should download a valid PDF file.

**What went wrong?**

Chrome reports: "Failed - Network error". That is however not true.

TLDR; Chrome can not base64 encode a file that is not in ASCII

I am using the FileReader readAsDataURL method to base64 encode the PDF file and add that to a hidden link element. This works with example.pdf which appears to be in ASCII. But utf8.pdf which is written in Norwegian fails with "Failed - Network error".

No errors are thrown.

I have also tried to create the blob myself with `new Blob([text], {encoding:"UTF-8",type:"application/pdf;charset=UTF-8"})` where `text` is the return value of text method of the Response interface of the Fetch API. This result in a file download but the PDF file is corrupted.

**Any other comments?**

In Firefox, the base64 text starts with `data:application/pdf; charset=utf-8;base64,` and result in a valid PDF file download.
But in Chrome the base64 text starts with `data:application/pdf;base64,` and fails.

The reduced test case can also be found at https://github.com/dotnetCarpenter/FileReader_Chrome
