How to make an asyncrhronous http request with DOHttpClient.

# Introduction #

This is an example code segment to make request with DOHttpClient.
Also in this example we are changing timeout values and request parameters.

# Details #

```
DOHttpClientRequestParameters clientParameters = new DOHttpClientRequestParameters();
clientParameters.add("operation", "getcustomers");
        
DOHttpClient client = new DOHttpClient();
client.setResponseListener(this);
client.setRequestMethod(DOHttpClientRequestMethod.POST);
client.setTimeoutConnection(10000);
client.setTimeoutData(10000);
client.setUrl("http://www.mysite.com/Service.aspx");
client.setParameters(clientParameters);
client.execute();
```

and you must implement OnDOHttpClientResponseListener interface in your Activity or other class. So you must implement two other method for handling the response coming from DOHttpClient.

```
@Override
public void onClientResponseSuccess(Object sender, HttpResponse response) {
	// you can use utility class for converting response to string.
	String content = DOHttpClientUtil.convertResponseToString(response); 
		
	Log.d("client", "success > " + content);
}

@Override
public void onClientResponseFault(Object sender, Exception e) {
	Log.d("client", "fault > " + e.getMessage());
}
```