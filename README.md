# PDF Signer Latest

A JavaScript PDF signer with certificate for NodeJS using .pfx. 

This package is fork of [vizicsaba89/pdf-signer](https://github.com/vizicsaba89/pdf-signer).

## PDF versions
Pdf-signer cant handle pdf stream in the moment. It only can works with pdf which built on XREF tables. 

## Document Signer Certificate
Document Signer Certificates are issued to organizational software applications for the automatic bulk authentication of documents/information attributed to the organization using digital signatures. This certificate is on the more expensive side and only issued to organizations. The most common uses for this type of signature are e-commerce receipts, invoices, credit card bills, etc.

## Installation

Installation uses the npm package manager. Just type the following command after installing npm.

```bash
npm install pdf-signer-latest
```

## Usage

single signing example:
```javascript
import { sign } from 'pdf-signer-brazil'
const fs = require('fs')
const dateFormat = require("dateformat")

const p12Buffer = fs.readFileSync(`./assets/pdf-signer.p12`) // CPF/CNPJ A1 ICP-Brasil: Use original .pfx file 
const pdfBuffer = fs.readFileSync(`./assets/example.pdf`)

const signature = 'Your Name'
const password = 'pdfsigner'
const signedPdf = sign.sign(pdfBuffer, p12Buffer, password, {
  reason: '2',
  email: 'test@mail.com',
  location: 'City, IN',
  signerName: signature,
  annotationAppearanceOptions: {
    signatureCoordinates: { left: 20, bottom: 120, right: 190, top: 20 },
    signatureDetails: [
      {
        value: signature,
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 32 },
      },
      {
        value: 'Name of the organization',
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 25.4 },
      },
      {
        value: 'Signed on' + dateFormat(new Date(), 'd/mm/yyyy HH:MM:ss'),
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 18 },
      },
      {
        value: 'This document is digitally signed by OZ',
        fontSize: 5,
        transformOptions: { rotate: 0, space: 2, tilt: 0, xPos: 0, yPos: 11 },
      },
    ]
  },
})
signedPdf.then(content => fs.writeFileSync('./assets/results/signed.pdf', content))
```
More examples can be found in spec file [spec](https://github.com/saiarlen/pdf-signer-latest/blob/master/src/sign.spec.ts).

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
