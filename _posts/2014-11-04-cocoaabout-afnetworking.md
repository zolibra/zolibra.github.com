---
layout: post
title: "[cocoa]About AFNetworking"
description: ""
category: 
tags: [AFNetworking,iOS,cocoa]
---
{% include JB/setup %}





typlically you are willing to send a POST request with JSON format:

    NSURL *url = [NSURL URLWithString:_baseUrl];
    AFHTTPClient *httpClient = [[AFHTTPClient alloc] initWithBaseURL:url];
    NSMutableURLRequest *request = [myClient requestWithMethod:@"POST" path:nil parameters:nil];
    
Pay attention that , if you specify path in the NSMutableURLRequest, the path in BaseURL will be ignore, for example:
	you have baseURL: http://192.168.1.100:8080/home/test, and you are willing to add a path 'test1'also in the NSMutableURLRequest's path, the resource path in baseURL will be ignore and request url will be :
	http://192.168.1.100:8080/test1
	
	
	