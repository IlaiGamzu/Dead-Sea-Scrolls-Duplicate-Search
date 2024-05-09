# Dead Sea Scrolls Duplicate Search

Hello every one,
This project talk about to found duplicate dead sea scrolls (by the content).
Each duplicate scroll could be a part from a big scroll or an independency scroll.

Note: This project code is on private repo, to get the code you need my permission- to get it please send me an email: Ilai.gamzu13@gmail.com

# How to solve the problem?
- First I use in YOLOV8 to detect each scroll
- After that I isolate each scrolls by the labels and the coordination of bounding box
- Finally I use in OCR and Sentence Transformers library to compare between scrolls.

# Step 1- Preapre to YOLOV8
- Before I used in YOLOV8n I need to labels the part of train and val from dataset:
- I used in labelimg (open source) that helps me to put labels and bounding box on my train and val.
- The labels and bounding box coordinate save on the picture_name.txt file (under a labels dir).

- how to divide the sub-scrolls?
- This question is very intersting, beacuse there is a lot of ways to decide "what is the optimal sub-scroll"
- For me, I chose to divide 

# YOLO V8n- The Model & Results
- To use in YOLOV8, first I need to resize my dataset to 320*320, beacuse the YOLO doesn't work well with high resolution.
- Then I made a yaml file that make the configiration of yolo model
- Finally I trained the model and the results is:
- Graphs:
  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/352b4595-007b-4ea6-9bdc-0d5e2434c7e3)

  Matrix_confusing:
  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/dfb2d5e1-f167-4e91-bc2b-d5f1b391595d)

  Predict:
  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/46d8cbcf-8e1d-49f4-93d7-430b847be8f3)

- As you can see the yolov8 success in 77%, the pick on the val means that I need to add more data.

# Step 2- Isolate images 
- After I have the bounding box coordinate for train, val, and test- I isolate each scroll in a new pictures 

