# CFNTechnical

Firstly thank you for taking the time to review and consider the enclosed work. I genuinely appreciate it! Also forgive my GitHub handle, this is a very old account :) 

To run this template and interact with the resulting resources requires the following. 
* Name your stack
* Supply a name without the presence of whitespace or special chars. 
* Supply your email and accept the topic subscription sent to the address you provide. 
* You can then test the Api by posting to the endpoint within the output of your CFN deployment, adhering to the model schema which can be found in API Gateway. Please note that only new PUTS will register in the stream, thus invoking SNS. 

Example: 
$ curl -X POST \\ 
  
  https://<api-id>.execute-api.<aws-region>.amazonaws.com/v1/add_new \\ 
  
  -H 'Content-Type: application/json' \\ 
  
  -H 'cache-control: no-cache' \\ 
  
  -d '{"team_rating":"1","team_country":"Ireland","team_desc":"better at rugby then Aus","team_name":"Ireland"}'

Improvements: 
The main improvements centre around the prinicples of least privilege as well as defence in depth. All layers of the deployed architecture shoud be protected against potential compromise. Should comprimise take place, the blast radius should be minimized as much as is possible. With that in mind I believe I have upgraded this template. This was done by restricting resources to invoking and consuming only the services needed and no more. Whether that be explicitly dictating the stream which should be used as an event trigger for Lambda or by limiting the CRUD operations available to a given Lambda execution against DynamoDB or any data store for that matter. 

Ideally, this template would have an Authenticated API either using a Lambda, Cognito or IAM Authorizer[1]. For relative certainty that common exploits are mitigated against, the API could be deployed behind a WAF[2]. This would both defend in earnest against any would be attacker and minimize the avenues of attack available should the perimiter be breached. 

I look forward to speaking with you. 

[1] Authentication for API Gateway https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-to-api.html
[2] WAF https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-aws-waf.html
