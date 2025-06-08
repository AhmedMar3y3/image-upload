Image Upload Package
A Laravel package for handling image uploads in your applications.
Installation
You can install the package via Composer:
composer require mar3y/image-upload

Requirements

PHP 7.4, 8.0, 8.1, 8.2, or 8.3
Laravel 8, 9, 10, 11, or 12
The public disk configured in config/filesystems.php
Run php artisan storage:link to link the public/storage directory

Usage
Using the HasImage Trait
To use the HasImage trait in your model, follow these steps:

Add the trait to your model class:
use mar3y\ImageUpload\Traits\HasImage;

class YourModel extends Model
{
    use HasImage;

    protected $fillable = ['image'];
    protected static $imageAttributes = ['image'];
}


Define the image attributes:
 In your model, define the $imageAttributes property as an array of attribute names that will store image paths. For example, protected static $imageAttributes = ['image', 'logo', 'banner'];.

Upload an image:
 When you save a model instance with an image attribute set to an UploadedFile instance, the trait will automatically upload the image and store the path.
$model = new YourModel();
$model->image = $request->file('image');
$model->save();


Retrieve the image URL:
 Access the full URL of the image using the attribute name.
$imageUrl = $model->image; // e.g., http://yourdomain.com/storage/images/yourmodel/xyz.jpg



Using the ImageUploadHelper
You can also use the ImageUploadHelper class directly:
use mar3y\ImageUpload\Helpers\ImageUploadHelper;

$path = ImageUploadHelper::uploadImage($file, 'your-directory');

Troubleshooting

Images not accessible: Ensure you’ve run php artisan storage:link and the public disk is configured in config/filesystems.php.
Class not found: Verify that Composer autoloading is set up correctly by running composer dump-autoload.
Relative URLs in API responses: Check that your model uses the HasImage trait and defines $imageAttributes.

Contributing
Contributions are welcome! Please submit a pull request or open an issue on GitHub.
License
The MIT License (MIT). See License File for more information.
