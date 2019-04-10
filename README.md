# RadiAssist
### A mammogram classifier to assist radiologists in quickly determining and diagnosing breast cancer.

## Inspiration
Hundreds of thousands of women are diagnosed with breast cancer each year, with the majority of these diagnoses coming from mammograms. To determine whether there is a malignant or benign growth in breast tissue, a radiologist must closely examine mammograms from different angles. Both computers and humans make mistakes, but I believe that by combining preliminary predictions from computers with conclusive diagnoses by humans, breast cancer can be efficiently and accurately detected.

## What it does
Using a simple web application, a "radiologist" (i.e. User) will log into the program and click on pre-uploaded mammograms that they wish to have classified. After clicking the "Predict" button, the photo data will be sent to the Microsoft Custom Vision AI platform to run on the trained model. The result will then be returned to the program and displayed on a new page, with the predicted result compared to the actual result. 

In theory, the program would allow the user to upload a picture and would only return predicted results. However, for the sake of the demo and to show the accuracy of the classifier, the program will compare the final results to the known results.

## How I built it
RadiAssist uses node.js, express.js, JavaScript, HTML/CSS, and Microsoft Custom Vision AI. I started with the webapp template provided by AthenaHacks and tweaked the program from there. The data was retrieved from the [Cancer Imaging Archive](https://wiki.cancerimagingarchive.net/display/Public/CBIS-DDSM) and contained ~170 GB of images and metadata in a Digital Imaging and Communications in Medicine (DICOM/DCM) format. CSVs were also available with information for each set of pictures. 

After downloading the data, I wrote Python scripts to rename the files, iterate through the CSVs, separate the images into folders based on their malignant/benign classification, and transform the images from .DCM to .PNG file format. Since Custom Vision limits file sizes to 6 MB and since the files contained words and extraneous material on the edges, I used Click 2 Crop to manually crop the mammograms of benign and malignant mass-only tumors. 

After training the data on Microsoft's Custom Vision, I wrote the REST api calls to send test photos and receive the results to display on the webpage.

## Challenges I ran into
The data itself was one of the biggest challenges, with a combined size of ~170 GB. Simply downloading the data took many hours (and should have been started prior to the hackathon). Once the data was on my computer, I had to separate and manually crop the files which took many more hours of focused work. 

Additionally, I ran into some issues with sending the image to the classifier (I had to upload the images to a private link on Imgur.com) and manipulating the returned data from the model. I have had only minor experience with web development, so actually being able to switch pages, access a model, and return the result was extremely challenging for me (shoutout to Stackoverflow for the help!).

Although I attempted to join teams with other ideas, I realized that I really wanted to execute my idea for a ML-classifier of mammograms. Thus the largest challenge for me, in addition to the data, was the time. Coding, debugging, data-cleaning, and writing this description all could have been completed much earlier had I had other team mates to share the work with. In the end, though, I'm glad that I got to carry out my idea and implement it into a final working prototype.

## Accomplishments that I'm proud of
One of the biggest things I'm proud of is that the program (and the trained model) actually work! I was worried that after spending hours and hours toiling through the data, that Microsoft's Custom Vision wouldn't be able to differentiate between the different classifications of mammograms.

This is also my first hackathon where I have worked on one project during the entire session and have produced a (somewhat) finished project to present at the demo!!

## What I learned
I had the chance to learn more about web applications (such as JavaScript/JQuery) and breast cancer radiology (in general). Using computer science to improve medicine interests me greatly (so much so that I'll be starting my Master's next year in Biomedical Computing!), and I'm happy that I had the chance to learn more about a sub-field in this area. Before starting this project, mammogram analysis was completely foreign to me and this project allowed me to research this topic in much greater detail.

## What's next for RadiAssist
More features, cleaner UI/UX, and an actual working log-in are all on the horizon for this app. Currently, the results page is not working correctly, so this will be fixed as well. I also plan to add more data, including images of calcification and not just masses. 

The current main function classifies breast tissue samples into either benign or malignant tumors. However, additional features such as breast density (1-4), subtlety of the abnormality (0-5), and shape of tumor could all be integrated into the model for better and more descriptive classification. For example, breast density can cause issues during routine screenings, as denser tissue can lead to false positives when diagnosing breast cancer. Thus if the model can predict that the tissue is denser than normal, the radiologist can take the necessary steps (such as ordering different tests) to ensure correct diagnosis. 

