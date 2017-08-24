
### These functions will solve the inverse of a matrix, store it in a cache, then if the same inverse is called again it will retrieve it from the cache rather than recalculate it.
```
`##` Solves inverse of matrix and stores it

makeCacheMatrix <- function(x = matrix()) {
      i <- NULL
      set <- function(y){
            x <<- y
            i <<- NULL
            }
      get <- function() x
      setinverse <- function(solve) i <<- solve
      getinverse <- function() i
      list(set=set,get=get,setinverse=setinverse,getinverse=getinverse)
}

`##` Checks if inverse exists in cache and returns it, otherwise calculates inverse

cacheSolve <- function(x, ...) {
      i <- x$getinverse()
      if(!is.null(i)) {
            message("getting cached data")
            return(i)
            }
      data <- x$get()
      i <- solve(data, ...)
      x$setinverse(i)
      i
}


## Return a matrix that is the inverse of 'x'

##  x <- makeCacheMatrix(rbind(c(1,3),c(3,1)))
##  cacheSolve(x)
##  > cacheSolve(x)
##        [,1]   [,2]
##  [1,] -0.125  0.375
##  [2,]  0.375 -0.125
##  > cacheSolve(x)
##  getting cached data
##        [,1]   [,2]
##  [1,] -0.125  0.375
##  [2,]  0.375 -0.125
