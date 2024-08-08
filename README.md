# Card-suit-identifier-with-AI

 This program can recognize the difference between any heart and any spade in a card of deck



## The Algorithm
Simply put the algorithm works by having a main folder and three sub folders in that main folder(train,val,test). You put your data sets in each one of these folders, but in different amounts, you should have the most in train because it trains the model, the second most in val because that is what's used to check if it's right, and the least in test because those are only need to test your program on. You then run a series of commands listed below to train the model(resnet.18) on your data set. After you have trained it you export it to onnox and test it to see if it works.

## Running this project

First you need to train a network to work with your dataset
Change directories into jetson-inference/python/training/classification/data
Download your dataset
Unzip your data set if it is a zip file if not skip this step
cd back to nvidia/jetson-inference/
run ./docker/run.sh
From inside the Docker container, change directories so you are in jetson-inference/python/training/classification
Run the training script to re-train the network where the model-dir argument is where the model should be saved and where the data is: python3 train.py --model-dir=models/cards data/cards
Exporting the network to run your program
Make sure you are in the docker container and in jetson-inference/python/training/classification
python3 onnx_export.py --model-dir=models/cards
Exit the docker container by pressing Ctl + D.
On your nano, navigate to the jetson-inference/python/training/classification directory.
ls models/cards/
NET=models/cards
DATASET=data/cards
imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/clubs/2_of_clubs.png output.png
https://www.youtube.com/watch?v=aQKR0SluVu8
