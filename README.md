# Tensorflow Project Templete
A simple and well designed OOP structure is essential for any Deep Learning project, so after a lot of practice and contributing in tensorflow projects here's a tensorflow project templete that combines   **simplcity**, **best practice for folder structure** and **good OOP design**.
The main idea is that there's much stuff you do every time you start your tensorflow project so wrapping all this shared stuff will help you to get into the main project faster.

# Table Of Content

-  [In a Nutshell](https://github.com/Mrgemy95/Tensorflow-Project-Templete#project-architecture)
-  [In Details](https://github.com/Mrgemy95/Tensorflow-Project-Templete#project-architecture)
    -  [Project architecture](https://github.com/Mrgemy95/Tensorflow-Project-Templete#project-architecture)
    -  [Folder structure](https://github.com/Mrgemy95/Tensorflow-Project-Templete#folder-structure)
    -  [ Main Components](https://github.com/Mrgemy95/Tensorflow-Project-Templete#main-components)
        -  [Model](https://github.com/Mrgemy95/Tensorflow-Project-Templete#model)
        -  [Trainer](https://github.com/Mrgemy95/Tensorflow-Project-Templete#ptrainer)
        -  [Data Loader](https://github.com/Mrgemy95/Tensorflow-Project-Templete#data-loader)
        -  [Logger](https://github.com/Mrgemy95/Tensorflow-Project-Templete#logger)
        -  [Configration](https://github.com/Mrgemy95/Tensorflow-Project-Templete#configration)
        -  [Main](https://github.com/Mrgemy95/Tensorflow-Project-Templete#main)
 -  [references](https://github.com/Mrgemy95/Tensorflow-Project-Templete#references)

# In a Nutshell
In a nutshell here's how to use this templete, assume you want to implement vgg model so you should do the following:
- Create a class named VGG in models folder that inherit the "base_model" class
- Override these two functions "build_model" where you implement the vgg model, and "init_saver" where you define a tensorflow saver, then call them in the initalizer.
- Create a VGG trainer in trainers folder that inherit from "base_train" class
- Override these 2 functions "train_step", "train_epoch" where you write the logic of the training process
- Create your main file where you create instance of the following objects "Model", "Logger", "Data_Generator", "Trainer", and config
- Pass the all these objects to the trainer object, and start your training by calling "trainer.train()" 

**You will a templete file and a simple example in the model and trainer folder that shows you how to try your first model simply.** 


# In Details

Project architecture 
--------------

<div align="center">

<img align="center" hight="600" width="600" src="https://github.com/Mrgemy95/Tensorflow-Project-Templete/blob/master/figures/diagram.png?raw=true">

</div>


Folder structure
--------------

```
├──  base
│   ├── base_model.py   - this file contains the abstract class of the model.
│   └── ease_trainer.py - this file contains the abstract class of the trainer.
│
│
├── model               -This folder contains any model of your project.
│   └── xample_model.py
│
│
├── trainer             -this folder contains trainers of your project.
│   └── example_trainer.py
│   
├──  mains              - here's the main/s of your project (you may need more than one main.
│                         
│  
├──  data _loader  
│    └── data_generator.py  - here's the data_generator that responsiple for all data handling.
│ 
└── utils
     ├── logger.py
     └── any_other_utils_you_need

```


## Main Components

### Models
--------------
- #### **Base model**
    
    Base model is an abstract class that must be Inherited by any model you create, the idea behind this is that there's much shared stuff between all models.
    The base model contains:
    1. ***Save*** -This function to save a checkpoint to the desk. 
    2. ***Load*** -This function to load a checkpoint from the desk.
    3. ***Cur_epoch, Global_step counters*** -These variables to keep track of the curerent epoch and global step.
    4. ***Init_Saver*** An abstract function to inialize the saver used for saving and loading the checkpoint, ***Note***: override this function in the model you want to implement.
    5. ***Build_model*** Here's an abstract function to define the model, ***Note***: override this function in the model you want to implement.
- #### **Your model**
    Here's where you implement your model.
    So you should :
    1. Create your model class and Inherit the base_model class
    2. override "build_model" where you write the tensorflow model you want
    3. override "init_save" where you create a tensorflow saver to use it to save and load checkpoint
    4. call the "build_model" and "init_saver" in the initalizer.

### Trainer
--------------
- #### **Base trainer**
    Base trainer is an abstract class that just wrap the training process.
- #### **Your trainer**
     Here's what you shoulf implement in your trainer.
    1. Create your trainer class and Inherit the base_trainer class.
    2. override these two functions "train_step", "train_epoch" where you implement the training process of each step and each epoch.
### Data Loader
These class is responsiple for all data handling and processing and provide an easy interface that can be used by the trainer.
### Logger
This class is responsiple for the tensorboard summary, in your trainer create a dictionary of all tensorflow variables you want to summarize then pass this dictionary to logger.summarize().
### Configration
I use Json as configration method and then parse it, so write all configs you want then parse it using "utils/config/process_config" and pass this configration object to all other objects.
### Main
Here's where you combine all previous part.
1. Parse the config file.
2. Create a tensorflow session.
2. Create an instance of "Model", "Data_Generator" and "Logger" and parse the config to all of them.
3. Create an instance of "Trainer" and pass all previous objects to it.
4. Now you can train your model by calling "Trainer.train()"


# Future Work
- Replace the data loader part with new tensorflow dataset API.

#Contributing
Any kind of enhancement, or contribution is welcomed.
