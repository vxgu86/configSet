ImageRequest(const std::string& camera_name_val, ImageCaptureBase::ImageType image_type_val, bool pixels_as_float_val = false, bool compress_val = true)
        {
            camera_name = camera_name_val;
            image_type = image_type_val;
            pixels_as_float = pixels_as_float_val;
            compress = compress_val;
        }
