# PHP Pwinty

A PHP implementation of the Pwinty HTTP API v2

Based on an implementation of API v1 by Brad Pineau

## Installation

Declare the following 3 variables:

	define("PWINTY_API", 		"sandbox");		// set to "production" or "sandbox"		
	define("PWINTY_MERCHANTID", "*******");		// available from pwinty.com
	define("PWINTY_APIKEY", 	"*******"); 	// available from pwinty.com

Add this line to your application:

    require_once("/PHPPwinty/PHPPwinty.php");

Declare a new instance of PHPPwinty

	$pwinty = new PHPPwinty();

## Example Usage

Catalogue

	$catalogue = $pwinty->getCatalogue(
		"GB",				//country code
		"Pro"				//quality
	);

Countries

	$countries = $pwinty->getCountries();	

Orders

	//gets all orders
	$order = $pwinty->getOrder(); 

	//gets one order
	$order = $pwinty->getOrderStatus("1234"); 

	//creates a new order
	$order = $pwinty->createOrder(
		"Chuck Norris", 	//name
		"123 Some Road", 	//address1
		"Some place", 		//address 2
		"Some town", 		//town
		"Some state", 		//state
		"12345", 			//postcode or zip
		"GB", 				//country code
		"GB", 				//destination code
		true, 				//tracked shipping
		"InvoiceMe", 		//payment method
		"Pro"				//quality
	);

	//updates an order
	$order = $pwinty->updateOrder(
		"1234",				//order id
		"Chuck Norris", 	//name
		"123 Some Road", 	//address1
		"Some place", 		//address 2
		"Some town", 		//town
		"Some state", 		//state
		"12345", 			//postcode or zip
	);

	//change order status
	$pwinty->updateOrderStatus(
		"1234, 				//orderid
		"Cancelled"			//status
	);

	//get order status
	$order = $pwinty->getOrderStatus(
		"1234"				//order id
	);

Photos
	
	//gets information about photos for an order
	$photos = $pwinty->getPhotos(
		"1234"				//order id
	);

	//gets information about a single photo
	$photo = $pwinty->getPhotos(
		"1234",				//order id
		"123456"			//photo id
	);

	//adds a photo
	$pwinty->addPhoto(
		"1234", 							//order id
		"4x6", 								//print size
		"http://www.mysite.com/photo.jpg", 	//image url
		"1", 								//print quantity
		"ShrinkToFit", 						//resize method
		"2000", 							//price to user
		"811cc87f4f77d6c33d638f9def39473b", //md5 hash
		"ewhweo42ufh2woed45f2sdf4yt5sdufw"	//file
	);								

	//delete a photo
	$pwinty->deletePhoto(
		"1234",				//order id
		"123456"			//photo id
	);