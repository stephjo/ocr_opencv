# ocr_opencv
we’ll apply OpenCV’s EAST text detector to detect the presence of text in an image. The EAST text detector will give us the bounding box (x, y)-coordinates of text ROIs.

We’ll extract each of these ROIs and then pass them into Tesseract v4’s LSTM deep learning text recognition algorithm.

The output of the LSTM will give us our actual OCR results.

Finally, we’ll draw the OpenCV OCR results on our output image.

When calling the tessarct  command under pytessaract library we need to supply a number of flags. The three most important ones are -l , --oem , and --psm .

The -l  flag controls the language of the input text. We’ll be using eng  (English) for this example but you can see all the languages Tesseract supports here.

The --oem  argument, or OCR Engine Mode, controls the type of algorithm used by Tesseract.

#OCR Engine Modes 
$ tesseract --help-oem
OCR Engine modes:
  0    Legacy engine only.
  1    Neural nets LSTM engine only.
  2    Legacy + LSTM engines.
  3    Default, based on what is available.
##We will use --oem 1  to indicate the deep learning LSTM engine.

#Page segmentation modes
$ tesseract --help-psm
Page segmentation modes:
  0    Orientation and script detection (OSD) only.
  1    Automatic page segmentation with OSD.
  2    Automatic page segmentation, but no OSD, or OCR. (not implemented)
  3    Fully automatic page segmentation, but no OSD. (Default)
  4    Assume a single column of text of variable sizes.
  5    Assume a single uniform block of vertically aligned text.
  6    Assume a single uniform block of text.
  7    Treat the image as a single text line.
  8    Treat the image as a single word.
  9    Treat the image as a single word in a circle.
 10    Treat the image as a single character.
 11    Sparse text. Find as much text as possible in no particular order.
 12    Sparse text with OSD.
 13    Raw line. Treat the image as a single text line,
       bypassing hacks that are Tesseract-specific.
       
##For OCR’ing text ROIs we can use modes 6  and 7, but if you’re OCR’ing large blocks of text then you may want to try 3 , the default mode.    ## We can try to adjust the --psm value if we are getting incorrect OCR results.
