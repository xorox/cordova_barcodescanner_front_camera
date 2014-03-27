cordova_barcodescanner_front_camera
===================================

En enhancement of the cordova barcodescanner plugin to use the front camera of an iPad.

To use the front camera, you just have to enhance the file CDVBarcodeScanner.mm in the plugins directory:

```
//--------------------------------------------------------------------------
//Check if there is a front camera available and usable, if yes, it uses that as frontCamera object
//--------------------------------------------------------------------------
- (AVCaptureDevice *)frontCamera {
    NSArray *devices = [AVCaptureDevice devicesWithMediaType:AVMediaTypeVideo];
    for (AVCaptureDevice *device in devices) {
        if ([device position] == AVCaptureDevicePositionFront) {
            return device;
        }
    }
    return nil;
}
```

On line 331 in the file CDVBarcodeScanner.mm replace the default device selection with the frontCamera function result:

```
    //AVCaptureDevice* device = [AVCaptureDevice defaultDeviceWithMediaType:AVMediaTypeVideo];
    AVCaptureDevice *device = [self frontCamera];
    if (!device) return @"unable to obtain video capture device";
```



That's basically it.



