---
layout: post
comments: true
categories: spring
---


## Request/Response paramters in spring method

* HttpSession
* **@PathVariable** annotated parameters for access to URI template variables.
```
@RequestMapping(value="/owners/{ownerId}", method=RequestMethod.GET)
public String findOwner(@PathVariable String ownerId, Model model) {
  Owner owner = ownerService.findOwner(ownerId);  
  model.addAttribute("owner", owner);  
  return "displayOwner"; 
}
```
* **@RequestHeader** annotated parameters for access to specific Servlet request HTTP headers.
* **@RequestBody** annotated parameters for access to the HTTP request body.
```
@RequestMapping(value = "/something", method = RequestMethod.PUT)
public void handle(@RequestBody String body, Writer writer) throws IOException {
  writer.write(body);
}
```
* **@RequestPart** annotated parameters for access to the content of a "multipart/form-data" request part.
```
@RequestMapping(value="/someUrl", method = RequestMethod.POST)
public String onSubmit(@RequestPart("meta-data") MetaData metadata,
                       @RequestPart("file-data") MultipartFile file) {
    // ...

}
```

* **HttpEntity<?>** parameters for access to the Servlet request HTTP headers and contents.

```
@RequestMapping("/something")
public ResponseEntity<String> handle(HttpEntity<byte[]> requestEntity) throws UnsupportedEncodingException {
  String requestHeader = requestEntity.getHeaders().getFirst("MyRequestHeader"));
  byte[] requestBody = requestEntity.getBody();
  // do something with request header and body

  HttpHeaders responseHeaders = new HttpHeaders();
  responseHeaders.set("MyResponseHeader", "MyValue");
  return new ResponseEntity<String>("Hello World", responseHeaders, HttpStatus.CREATED);
}
```