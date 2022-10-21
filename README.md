# fetching-data
ublic boolean send() {
    Client client = ClientBuilder.newBuilder().build();
    WebTarget target = client.target(
            "http://localhost:8080/backend_war_exploded/user/register"
    );

    // this = class Registration 
    Entity entity = Entity.entity(this, MediaType.APPLICATION_JSON);

    try {
        Registration registration = target
                .request()
                .post(
                        entity,
                        Registration.class
                );
    } catch (Exception e) {
        e.printStackTrace();
        return false;
    }
    return true;
}

And on the server side:

@RequestMapping(
        value = "/register",
        method = RequestMethod.POST,
        headers = "Accept=application/json",
        produces = "application/json"
)
public ResponseEntity<SystemUser> create(
        @RequestBody SystemUser body
) {
    ResponseEntity<SystemUser> responseEntity = new ResponseEntity<>(
        systemUserService.create(body), HttpStatus.CREATED
    );
    return responseEntity;
