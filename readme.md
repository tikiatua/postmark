# Postmark module
Convenience wrapper for the postmarkapi.com email service. An example of the 
usage is given below. Batch email sending and postmark templates are also 
supported. The package does not depend on any other packages outside the standard
go library.

```golang
import (
	"fmt"
	"log"

	"github.com/dkfbasel/postmark"
)

func ExampleService() {

	// initialize the service
	mailer, err := postmark.New(postmark.DefaultHost, postmark.TestApiKey,
		postmark.Address("DKFBasel", "info@dkfbasel.ch"))

	if err != nil {
		log.Fatalf("could not initialize postmark service: %+v\n", err)
	}

	// compose a new message, use postmark.Emails for multiple email addresses
	// or postmark.Addresses for multiple addresses
	message := postmark.Message{
		To:       postmark.Emails("someone@dkfbasel.ch", "someone-else@dkfbasel.ch"),
		Subject:  "This is a subject",
		TextBody: "MESSAGE-BODY-AS-TEXT",
	}

	// send the message through the postmark service
	response, err := mailer.Send(&message)

	if err != nil {
		log.Fatalf("could not send the message: %+v\n", err)
	}

	fmt.Printf("%#v\n", response)
}
```