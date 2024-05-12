# Dead Sea Scrolls Duplicate Search

Hello everyone,

This project focuses on finding duplicate Dead Sea Scrolls by their content. Each duplicate might be part of a larger scroll or an independent scroll.

# Notes before start: 
1. The project code is in a private repository. To access the code, please email me for permission at: Ilai.gamzu13@gmail.com or in my linkdin https://www.linkedin.com/in/ilai-gam-zu-letova-a78915245.
2. The data-set does not uploaded, beacise it is belong to my collage.

# How to Solve the Problem?
- Initially, I use YOLOv8 to detect each scroll.
- Then, I isolate each scroll using the labels and coordinates from the bounding box.
- Finally, I use OCR and the Sentence Transformers library to compare the scrolls' content.
  
# Challenges Encountered
- Deleted letters make recognition more challenging.
- Determining which part of a scroll could be a duplicate within a larger scroll is complex.


# Step 1: Prepare for YOLOv8
- Before using YOLOv8, I needed to label the training and validation parts of the dataset.
- I used LabelImg, an open-source tool that helps to annotate images with labels and bounding boxes for my training and validation sets.
- The labels and bounding box coordinates are saved in the picture_name.txt file (under a labels directory).
  
# Dividing the Sub-scrolls
- Deciding how to optimally divide sub-scrolls is an interesting challenge, as there are many possible approaches.
- I chose to divide each scroll that appears as two pages into two separate scrolls and also to divide scrolls that contain distinct paragraphs like those shown in the images:

![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/26209885-b368-4e0d-b8d2-a313777aeab0)

![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/34f38fd6-d514-407b-98b3-190ae33762ec)
  

# YOLO V8: Model & Results
- I resized my dataset to 320x320 because YOLO does not perform well with high-resolution images.
- I configured the YOLO model using a YAML file, trained it, and obtained the following results:
  
- Graphs:
  
  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/352b4595-007b-4ea6-9bdc-0d5e2434c7e3)

  Matrix_confusing:
  
  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/dfb2d5e1-f167-4e91-bc2b-d5f1b391595d)

  Predict:
  
  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/46d8cbcf-8e1d-49f4-93d7-430b847be8f3)

- Graphs and confusion matrices show a 77% success rate, indicating a need for more data (data augmentation).

# Step 2: Isolate Images
- Using the bounding box coordinates from the train, validation, and test sets, I isolated each scroll into new images.

# Step 3: OCR
- Before using OCR, I processed each scroll to improve recognition—adjusting scaling, binarization, noise removal, etc.
- I used a model trained on Hebrew text to recognize the content of each scroll.
- I saved the OCR results in a dictionary and compared the vector features using cosine similarity.
  
# Model Evaluation
- To evaluate the model, I used a sanity check by duplicating two pictures and testing the model's recognition capability.
- The plots confirmed that the model could memorize effectively.
  
  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/4d9df81b-26bf-4b05-866a-eb346cc5ba89)


# Results on 200 Scrolls
- The model identified several similar scrolls when tested on 200 scrolls.

  ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/eb74185d-57d4-478d-81af-1dbc86e989a5)

- However, upon reviewing the images, it was evident that the model sometimes misidentified unclear letters as empty scrolls.
 
1. ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/887c1d5a-f792-4c45-8b36-af67ee4759e5)

2. ![image](https://github.com/IlaiGamzu/Dead-Sea-Scrolls-Duplicate-Search/assets/135164356/5229ae2d-03b9-4ca5-bccc-a81407d3984d)


# How to Improve Results?
- Optimize image processing to enhance OCR accuracy.
- Develop a new model specifically tailored to the scroll's font.




