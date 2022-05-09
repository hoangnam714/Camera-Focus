    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        if let touch = touches.first {
            let tapPoint = touch.location(in: vPreviewCapture)
            if vPreviewCapture.bounds.contains(tapPoint) {
                //Convert point from tap point to preview point
                let convertPoint = cameraController.previewLayer?.captureDevicePointConverted(fromLayerPoint: tapPoint)
                let device:AVCaptureDevice?
                if cameraController.currentCameraPosition == .front {
                    device = cameraController.frontCamera }
                else {
                    device = cameraController.rearCamera
                }
                
                do {
                    guard let device = device, let convertPoint = convertPoint else {
                        print("No suport")
                        return
                    }
                    try device.lockForConfiguration()
                    device.focusPointOfInterest = convertPoint
                    device.focusMode = .autoFocus
                    device.exposurePointOfInterest = convertPoint
                    device.exposureMode = .continuousAutoExposure
                    device.unlockForConfiguration()
                } catch {
                    print("Can't focus object")
                }
                // Add sub edit view
                let _tapPoint = CGPoint(x: tapPoint.x - 25, y: tapPoint.y - 25)
                let subFocusView = UIView(frame: CGRect(origin: _tapPoint, size: CGSize(width: 50, height: 50)))
                subFocusView.layer.cornerRadius = 25
                subFocusView.layer.borderWidth  = 2
                subFocusView.layer.borderColor  = UIColor.white.cgColor
                subFocusView.layoutIfNeeded()
                vPreviewCapture.addSubview(subFocusView)
                
                UIView.animate(withDuration: 1, delay: 0, options: [.curveEaseInOut]) {
                    subFocusView.transform = CGAffineTransform(scaleX: 0.8, y: 0.8)
                } completion: { _ in
                    subFocusView.transform = CGAffineTransform.identity
                    subFocusView.removeFromSuperview()
                }
            }
        }
    }
