# Roshni-app

This is an Android application that recognizes the denomination of Indian currency notes using a smartphone camera. This has been designed to primarily assist visually impaired people in identifying Indian currency notes. I created this while doing my internship at IIT Ropar. Here is the playstore link to it: https://play.google.com/store/apps/details?id=com.Roshni.ipsa.myapplication

# My approach of training the weights 

The initial too ambitious but also minimum work approach failed quickly. It was to identify the rupee symbol using optical character recognition (OCR) as the rupee symbol is recognized as a digital symbol but this failed as it was not being recognized in any direction other than upright or when there was any blurring or overlay of any shade. Also I realized that when a note is held in a folded position the rupee symbol might not even be visible. Then there was a quick testing of the idea to use an object recognition model YOLO v2 to detect the rupee symbol and then because the denomination is written close to this symbol, have the OCR run on those few digits but this too ran into the same problems and the same would have happened with running OCR on the whole picture so it was not worth trying that. 

While trying the above approach, I realized that it would be better to have the whole note be treated as an object for object recognition to run on. And while clicking more pictures of the currency notes I realized that I should help object recognition by giving it more than one object to recognize in a frame. So I split each side (2 sides) of each note into 4 sections (depicted below) making them as 8 objects to recognize, any one of which would point to the same denomination. So this resulted in the creation of 8 classes per note (4 for the front side and 4 for the back). I then annotated the pictures (having a random background and a note in the foreground) with coordinates of the object present in it and its class from my 80 classes (because I had 8 types of denominations).

![alt text](https://github.com/MehulGoel1/Roshni-app/blob/main/images/Screenshot_12.png)
![alt text](https://github.com/MehulGoel1/Roshni-app/blob/main/images/Screenshot_11.png)

After a quick test of the above approach which passed well, I wanted to augment the image data. As there weren't too many scenarios possible in the real world usage I applied only a few image augmentation techniques accommodating the following scenarios and all combinations of them: different brightness, hue of the camera flash, shaky and blurry picture, and the note at different angles in the picture. To augment for different angles I had to click more pictures in outdoor lighting and in darkness with the flash on, as all my pictures until then were taken in indoor lighting and I could not simulate the other two scenarios well enough using any data augmentation libraries' functions. 

I could achieve 90% accuracy 

