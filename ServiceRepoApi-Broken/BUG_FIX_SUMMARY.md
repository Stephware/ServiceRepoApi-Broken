# 23 Bug Fix Summary

1. `[ApiController]` was missing, so I added it because API validation and binding needs it.
2. The base route made `/api/productss`, so I changed it to `/api/products` because the endpoint was wrong.
3. GET used `{productId}` but the parameter was `id`, so I matched them because the route value was not binding correctly.
4. Update used POST, so I changed it to PUT because update should use the correct HTTP verb.
5. Delete had no `{id}` in the route, so I added it because the API needs to know what product to delete.
6. The controller used `AppDbContext` directly, so I removed it and used the service because controllers should not access the database.
7. GET by id always returned 200, so I added 404 when missing because a missing product is not a successful request.
8. Create returned 200, so I changed it to 201 with `Location` because a new resource was created.
9. Update did not compare route id and body id, so I added the check because mismatched ids can update the wrong product.
10. Create duplicate checking was in the controller, so I moved it to the service because it is business logic.
11. Duplicate checking happened before trimming, so I trim first because spaces could bypass the duplicate rule.
12. Name trimming was done in the controller, so I moved it to the service because the rule belongs there.
13. `CreatedAt` was set in the controller using local time, so I moved it to the service and used UTC because the server should control creation time.
14. POST accepted the client `Id`, so I reset it to 0 because the server should assign the id.
15. Update returned success when the product was missing, so I return NotFound because nothing was updated.
16. Update had no duplicate-name check, so I added one excluding the same id because names must stay unique.
17. Update did not save `Description`, so I added it because all editable fields should update.
18. Update changed `CreatedAt`, so I stopped changing it because creation time must stay the same.
19. Delete was missing from the service, so I added `DeleteAsync` because delete rules should pass through the service.
20. Delete blocked stock 0 instead of stock above 0, so I reversed the rule because only zero-stock products can be deleted.
21. NotFound and Conflict statuses were wrong, so I fixed the mappings and `Conflict()` result because the API was returning wrong status codes.
22. Repository reads were wrong, so I removed `Take(10)` and used `SingleOrDefaultAsync` because all products must show and missing ids should not crash.
23. Repository Update marked products as `Added`, so I changed it to `Update` because editing should not insert a new row.
