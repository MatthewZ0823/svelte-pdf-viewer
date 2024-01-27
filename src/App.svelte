<script>
  import { PDFDocument } from 'pdf-lib';
  import mypdf from '$lib/shrek-script-pdf.pdf';

  let pdfDataUri;

  const loadPDF = async () => {
    try {
      // Convert the imported PDF file to a Uint8Array
      const response = await fetch(mypdf);
      const pdfArrayBuffer = await response.arrayBuffer();
      let pdfBytes = new Uint8Array(pdfArrayBuffer);

      // Now you can use pdfBytes as a Uint8Array containing the PDF file content
      const pdfDoc = await PDFDocument.load(pdfBytes);
      console.log(pdfDoc); // Do something with the loaded PDF document

      pdfDataUri = await pdfDoc.saveAsBase64({ dataUri: true });
    } catch (error) {
      console.error('Error loading PDF:', error);
    }
  };

  // Call the function to load the PDF when the component mounts
  loadPDF();
</script>

<!-- too lazy to figure out css -->
<iframe title="pdf" style="width: 100%; height: 100%;" src={pdfDataUri}></iframe>

<style>
</style>
