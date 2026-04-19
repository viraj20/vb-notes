





v3.map ---> web-le-app-production.web 

x-app-source= mobile-web ---> mobile-web-app

 events_path || plays_path || sports_path || activities_path || venues_path || concerts_path || festival_path || theater_path || not_found_path || merchandise_path || special_path ---> web-v3



	acl events_path path_reg ^/([a-zA-Z-]+)?/?events/?.*$
	acl plays_path path_reg ^/([a-zA-Z-]+)?/?plays/?.*$
	acl sports_path path_reg ^/([a-zA-Z-]+)?/?sports/?.*$
	acl activities_path path_reg ^/([a-zA-Z-]+)?/?activities/?.*$
	acl venues_path path_reg ^/([a-zA-Z-]+)?/?venue(/.*)?$
	acl venues_listing_path path_reg ^/([a-zA-Z-]+)?/?venues(/.*)?$
	acl concerts_path path_reg ^/([a-zA-Z-]+)?/?concerts/?.*$
	acl festival_path path_reg ^/([a-zA-Z-]+)?/?festival/?.*$
	acl theater_path path_reg ^/([a-zA-Z-]+)?/?theater/?.*$
	acl not_found_path path_beg /not-found
	acl merchandise_path path_reg ^/([a-zA-Z-]+)?/?merchandise/?.*$
	acl special_path path_reg ^/([a-zA-Z-]+)?/?special/?.*$


x-app-source = web-v3 ---> 



1. Validate and remove v3.map which are not required
2. Add remaining to CF transform rules and pass header x-app-source = web-le-app
3. For IPL and similar evenets add another transform rule with  x-app-source = web-v3
4. Change HAProxy to support above headers
5. Change 	use_backend %[path,map_reg(/usr/local/etc/haproxy/v3.map,backend_web_v3)] if events_path || plays_path || sports_path || activities_path || venues_path || concerts_path || festival_path || theater_path || not_found_path || merchandise_path || special_path in HaProxy to support mobile device and desktop device condition



