
### More details can be found in the original [README](https://github.com/gorilla/schema/blob/master/README.md)


### This fork adds the posibility to add default values when decoding using the `default` tag

The supported field for the `default` tag:

* bool
* float variants (float32, float64)
* int variants (int, int8, int16, int32, int64)
* string
* uint variants (uint, uint8, uint16, uint32, uint64)
* a pointer to one of the above types


## Example


```go
var decoder = schema.NewDecoder()

type Person struct {
    Name  string `schema:"name" default:"tester"`
    Phone string `schema:"phone" default:"+12345567895"`
}

func MyHandler(w http.ResponseWriter, r *http.Request) {
    err := r.ParseForm()
    if err != nil {
        // Handle error
    }

    var person Person

    // r.PostForm is a map of our POST form values
    err = decoder.Decode(&person, r.PostForm)
    if err != nil {
        // Handle error
    }

    //assuming name and phone are not provided
    //person.Name will have value: tester
    //person.Phone will have value: +12345567895
}
```







