base network final validation accuracy:
Epoch 50/50
390/390 [==============================] - 20s 51ms/step - loss: 0.2995 - acc: 0.9009 - val_loss: 0.5959 - val_acc: 0.8272
Model took 1009.45 seconds to train

Updated model.add:
model = Sequential()
####with depthwise seperable convolution; 
model.add(SeparableConvolution2D(48, 3, 3, border_mode='same', input_shape=(32, 32, 3))) # input: 32x32x3 output: 32x32x48
model.add(Activation('relu'))
model.add(BatchNormalization())
model.add(SeparableConvolution2D(48, 3, 3)) # 30x30x48
model.add(Activation('relu'))
model.add(BatchNormalization())
model.add(MaxPooling2D(pool_size=(2, 2)))  # 15x15x48
model.add(SeparableConvolution2D(96, 3, 3, border_mode='same')) # 15x15x96
model.add(Activation('relu'))
model.add(BatchNormalization())
model.add(SeparableConvolution2D(96, 3, 3)) #13x13x96
model.add(Activation('relu'))
model.add(BatchNormalization()) 
model.add(SeparableConvolution2D(192, 3, 3)) #11x11x192
model.add(Activation('relu'))
model.add(BatchNormalization()) 
model.add(SeparableConvolution2D(96, 3, 3)) #9x9x192
model.add(Activation('relu'))
model.add(BatchNormalization()) 
model.add(SeparableConvolution2D(96, 3, 3)) #7x7x96
model.add(Activation('relu'))
model.add(BatchNormalization()) 
model.add(SeparableConvolution2D(48, 3, 3))  # 5x5x48
model.add(Activation('relu'))
model.add(BatchNormalization())
model.add(Dropout(0.1))
model.add(SeparableConvolution2D(24, 3, 3))  # 3x3x24
model.add(Activation('relu'))
model.add(BatchNormalization())
model.add(SeparableConvolution2D(12, 3, 3))  # 1x1x12
model.add(Activation('relu'))
model.add(BatchNormalization())
#model.add(MaxPooling2D(pool_size=(2, 2))) #2x2x48
model.add(Dropout(0.1))
model.add(SeparableConvolution2D(10, 1, 1))  # 1x1x10
model.add(Activation('relu'))
model.add(BatchNormalization())
model.add(Dropout(0.15))
model.add(Flatten())
model.add(Activation('softmax'))
# Compile the model
model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])

Model: "sequential_10"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
separable_conv2d_74 (Separab (None, 32, 32, 48)        219       
_________________________________________________________________
activation_79 (Activation)   (None, 32, 32, 48)        0         
_________________________________________________________________
batch_normalization_73 (Batc (None, 32, 32, 48)        192       
_________________________________________________________________
separable_conv2d_75 (Separab (None, 30, 30, 48)        2784      
_________________________________________________________________
activation_80 (Activation)   (None, 30, 30, 48)        0         
_________________________________________________________________
batch_normalization_74 (Batc (None, 30, 30, 48)        192       
_________________________________________________________________
max_pooling2d_17 (MaxPooling (None, 15, 15, 48)        0         
_________________________________________________________________
separable_conv2d_76 (Separab (None, 15, 15, 96)        5136      
_________________________________________________________________
activation_81 (Activation)   (None, 15, 15, 96)        0         
_________________________________________________________________
batch_normalization_75 (Batc (None, 15, 15, 96)        384       
_________________________________________________________________
separable_conv2d_77 (Separab (None, 13, 13, 96)        10176     
_________________________________________________________________
activation_82 (Activation)   (None, 13, 13, 96)        0         
_________________________________________________________________
batch_normalization_76 (Batc (None, 13, 13, 96)        384       
_________________________________________________________________
separable_conv2d_78 (Separab (None, 11, 11, 192)       19488     
_________________________________________________________________
activation_83 (Activation)   (None, 11, 11, 192)       0         
_________________________________________________________________
batch_normalization_77 (Batc (None, 11, 11, 192)       768       
_________________________________________________________________
separable_conv2d_79 (Separab (None, 9, 9, 96)          20256     
_________________________________________________________________
activation_84 (Activation)   (None, 9, 9, 96)          0         
_________________________________________________________________
batch_normalization_78 (Batc (None, 9, 9, 96)          384       
_________________________________________________________________
separable_conv2d_80 (Separab (None, 7, 7, 96)          10176     
_________________________________________________________________
activation_85 (Activation)   (None, 7, 7, 96)          0         
_________________________________________________________________
batch_normalization_79 (Batc (None, 7, 7, 96)          384       
_________________________________________________________________
separable_conv2d_81 (Separab (None, 5, 5, 48)          5520      
_________________________________________________________________
activation_86 (Activation)   (None, 5, 5, 48)          0         
_________________________________________________________________
batch_normalization_80 (Batc (None, 5, 5, 48)          192       
_________________________________________________________________
dropout_44 (Dropout)         (None, 5, 5, 48)          0         
_________________________________________________________________
separable_conv2d_82 (Separab (None, 3, 3, 24)          1608      
_________________________________________________________________
activation_87 (Activation)   (None, 3, 3, 24)          0         
_________________________________________________________________
batch_normalization_81 (Batc (None, 3, 3, 24)          96        
_________________________________________________________________
separable_conv2d_83 (Separab (None, 1, 1, 12)          516       
_________________________________________________________________
activation_88 (Activation)   (None, 1, 1, 12)          0         
_________________________________________________________________
batch_normalization_82 (Batc (None, 1, 1, 12)          48        
_________________________________________________________________
dropout_45 (Dropout)         (None, 1, 1, 12)          0         
_________________________________________________________________
separable_conv2d_84 (Separab (None, 1, 1, 10)          142       
_________________________________________________________________
activation_89 (Activation)   (None, 1, 1, 10)          0         
_________________________________________________________________
batch_normalization_83 (Batc (None, 1, 1, 10)          40        
_________________________________________________________________
dropout_46 (Dropout)         (None, 1, 1, 10)          0         
_________________________________________________________________
flatten_9 (Flatten)          (None, 10)                0         
_________________________________________________________________
activation_90 (Activation)   (None, 10)                0         
=================================================================
Total params: 79,085
Trainable params: 77,553
Non-trainable params: 1,532
my 50 epoch logs:

Epoch 1/50
  2/390 [..............................] - ETA: 31s - loss: 0.8212 - acc: 0.7422/usr/local/lib/python3.6/dist-packages/ipykernel_launcher.py:12: UserWarning: The semantics of the Keras 2 argument `steps_per_epoch` is not the same as the Keras 1 argument `samples_per_epoch`. `steps_per_epoch` is the number of batches to draw from the generator at each epoch. Basically steps_per_epoch = samples_per_epoch/batch_size. Similarly `nb_val_samples`->`validation_steps` and `val_samples`->`steps` arguments have changed. Update your method calls accordingly.
  if sys.path[0] == '':
/usr/local/lib/python3.6/dist-packages/ipykernel_launcher.py:12: UserWarning: Update your `fit_generator` call to the Keras 2 API: `fit_generator(<keras_pre..., validation_data=(array([[[..., verbose=1, steps_per_epoch=390, epochs=50)`
  if sys.path[0] == '':
390/390 [==============================] - 21s 53ms/step - loss: 0.8334 - acc: 0.7144 - val_loss: 0.7887 - val_acc: 0.7350
Epoch 2/50
390/390 [==============================] - 21s 53ms/step - loss: 0.7948 - acc: 0.7285 - val_loss: 0.8243 - val_acc: 0.7317
Epoch 3/50
390/390 [==============================] - 21s 54ms/step - loss: 0.7665 - acc: 0.7387 - val_loss: 0.7861 - val_acc: 0.7459
Epoch 4/50
390/390 [==============================] - 21s 54ms/step - loss: 0.7235 - acc: 0.7513 - val_loss: 0.7542 - val_acc: 0.7612
Epoch 5/50
390/390 [==============================] - 21s 54ms/step - loss: 0.7000 - acc: 0.7577 - val_loss: 0.7913 - val_acc: 0.7467
Epoch 6/50
390/390 [==============================] - 21s 54ms/step - loss: 0.6755 - acc: 0.7648 - val_loss: 0.7703 - val_acc: 0.7589
Epoch 7/50
390/390 [==============================] - 21s 54ms/step - loss: 0.6607 - acc: 0.7705 - val_loss: 0.7815 - val_acc: 0.7499
Epoch 8/50
390/390 [==============================] - 21s 54ms/step - loss: 0.6299 - acc: 0.7813 - val_loss: 0.7565 - val_acc: 0.7637
Epoch 9/50
390/390 [==============================] - 21s 53ms/step - loss: 0.6075 - acc: 0.7880 - val_loss: 0.7932 - val_acc: 0.7575
Epoch 10/50
390/390 [==============================] - 21s 54ms/step - loss: 0.5890 - acc: 0.7945 - val_loss: 0.7885 - val_acc: 0.7595
Epoch 11/50
390/390 [==============================] - 21s 54ms/step - loss: 0.5764 - acc: 0.7998 - val_loss: 0.7701 - val_acc: 0.7646
Epoch 12/50
390/390 [==============================] - 21s 53ms/step - loss: 0.5549 - acc: 0.8028 - val_loss: 0.8254 - val_acc: 0.7574
Epoch 13/50
390/390 [==============================] - 21s 53ms/step - loss: 0.5374 - acc: 0.8086 - val_loss: 0.7839 - val_acc: 0.7703
Epoch 14/50
390/390 [==============================] - 21s 53ms/step - loss: 0.5162 - acc: 0.8172 - val_loss: 0.7914 - val_acc: 0.7677
Epoch 15/50
390/390 [==============================] - 21s 54ms/step - loss: 0.5066 - acc: 0.8193 - val_loss: 0.8176 - val_acc: 0.7661
Epoch 16/50
390/390 [==============================] - 21s 54ms/step - loss: 0.4985 - acc: 0.8224 - val_loss: 0.8033 - val_acc: 0.7664
Epoch 17/50
390/390 [==============================] - 21s 54ms/step - loss: 0.4830 - acc: 0.8268 - val_loss: 0.8104 - val_acc: 0.7657
Epoch 18/50
390/390 [==============================] - 21s 54ms/step - loss: 0.4767 - acc: 0.8291 - val_loss: 0.8384 - val_acc: 0.7628
Epoch 19/50
390/390 [==============================] - 21s 54ms/step - loss: 0.4603 - acc: 0.8335 - val_loss: 0.8439 - val_acc: 0.7652
Epoch 20/50
390/390 [==============================] - 21s 54ms/step - loss: 0.4474 - acc: 0.8362 - val_loss: 0.8587 - val_acc: 0.7597
Epoch 21/50
390/390 [==============================] - 21s 54ms/step - loss: 0.4503 - acc: 0.8373 - val_loss: 0.9341 - val_acc: 0.7556
Epoch 22/50
390/390 [==============================] - 21s 54ms/step - loss: 0.4215 - acc: 0.8457 - val_loss: 0.8870 - val_acc: 0.7622
Epoch 23/50
390/390 [==============================] - 21s 53ms/step - loss: 0.4234 - acc: 0.8431 - val_loss: 0.9024 - val_acc: 0.7621
Epoch 24/50
390/390 [==============================] - 21s 53ms/step - loss: 0.4254 - acc: 0.8455 - val_loss: 0.9262 - val_acc: 0.7553
Epoch 25/50
390/390 [==============================] - 21s 53ms/step - loss: 0.4083 - acc: 0.8476 - val_loss: 0.8572 - val_acc: 0.7746
Epoch 26/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3965 - acc: 0.8538 - val_loss: 0.8742 - val_acc: 0.7740
Epoch 27/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3904 - acc: 0.8539 - val_loss: 0.9055 - val_acc: 0.7635
Epoch 28/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3852 - acc: 0.8538 - val_loss: 0.8678 - val_acc: 0.7775
Epoch 29/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3810 - acc: 0.8565 - val_loss: 0.9343 - val_acc: 0.7533
Epoch 30/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3733 - acc: 0.8579 - val_loss: 0.9309 - val_acc: 0.7641
Epoch 31/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3733 - acc: 0.8585 - val_loss: 0.9246 - val_acc: 0.7668
Epoch 32/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3669 - acc: 0.8599 - val_loss: 0.9716 - val_acc: 0.7641
Epoch 33/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3626 - acc: 0.8625 - val_loss: 0.9613 - val_acc: 0.7665
Epoch 34/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3530 - acc: 0.8645 - val_loss: 0.9465 - val_acc: 0.7638
Epoch 35/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3402 - acc: 0.8663 - val_loss: 0.9880 - val_acc: 0.7583
Epoch 36/50
390/390 [==============================] - 21s 53ms/step - loss: 0.3459 - acc: 0.8672 - val_loss: 0.9378 - val_acc: 0.7720
Epoch 37/50
390/390 [==============================] - 21s 53ms/step - loss: 0.3345 - acc: 0.8707 - val_loss: 1.0063 - val_acc: 0.7609
Epoch 38/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3492 - acc: 0.8644 - val_loss: 0.9993 - val_acc: 0.7562
Epoch 39/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3381 - acc: 0.8686 - val_loss: 0.9880 - val_acc: 0.7640
Epoch 40/50
390/390 [==============================] - 21s 53ms/step - loss: 0.3324 - acc: 0.8699 - val_loss: 0.9924 - val_acc: 0.7625
Epoch 41/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3218 - acc: 0.8737 - val_loss: 1.0402 - val_acc: 0.7550
Epoch 42/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3230 - acc: 0.8736 - val_loss: 1.0053 - val_acc: 0.7692
Epoch 43/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3224 - acc: 0.8755 - val_loss: 1.0137 - val_acc: 0.7715
Epoch 44/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3187 - acc: 0.8765 - val_loss: 1.0266 - val_acc: 0.7620
Epoch 45/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3152 - acc: 0.8756 - val_loss: 1.0315 - val_acc: 0.7626
Epoch 46/50
390/390 [==============================] - 21s 53ms/step - loss: 0.3063 - acc: 0.8790 - val_loss: 1.0208 - val_acc: 0.7636
Epoch 47/50
390/390 [==============================] - 21s 53ms/step - loss: 0.3026 - acc: 0.8784 - val_loss: 1.0531 - val_acc: 0.7625
Epoch 48/50
390/390 [==============================] - 21s 53ms/step - loss: 0.3049 - acc: 0.8791 - val_loss: 1.1107 - val_acc: 0.7599
Epoch 49/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3081 - acc: 0.8780 - val_loss: 1.1502 - val_acc: 0.7436
Epoch 50/50
390/390 [==============================] - 21s 54ms/step - loss: 0.3099 - acc: 0.8768 - val_loss: 1.0794 - val_acc: 0.7645
Model took 1044.39 seconds to train

