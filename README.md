# gotest

test functions

```go
func IsLetter1(s string) bool {
	for _, r := range s {
		if !unicode.IsLetter(r) {
			return false
		}
	}
	return true
}

func IsLetter2(s string) bool {
	for _, r := range s {
		if (r < 'a' || r > 'z') && (r < 'A' || r > 'Z') {
			return false
		}
	}
	return true
}

var IsLetter3 = regexp.MustCompile(`^[a-zA-Z]+$`).MatchString

const alpha = "abcdefghijklmnopqrstuvwxyz"

func IsLetter4(s string) bool {
	for _, char := range s {
		if !strings.Contains(alpha, strings.ToLower(string(char))) {
			return false
		}
	}
	return true
}
```

go bench
```console
 go test -bench=.                    
goos: darwin
goarch: amd64
pkg: github.com/heshed/gotest
cpu: Intel(R) Core(TM) i9-9980HK CPU @ 2.40GHz
Benchmark/unicode.IsLetter-16           15167793                69.88 ns/op
Benchmark/check_azAZ_char-16            29699143                38.84 ns/op
Benchmark/RegularExpression-16           1505218               772.9 ns/op
Benchmark/check_lowercase-16             1322492               915.3 ns/op
PASS
ok      github.com/heshed/gotest        6.444s
```