all: scanner.c parser.c lemon

lemon: lemon.c
	$(CC) -O2 "$<" -o "$@"

scanner.c: scanner.re Makefile
	re2c -b -o "$@" "$<"
	sed -i 's!^#line.*$$!/* & */!g' "$@"
	sed -i 's/YY/JJ/g; s/yy/jj/g' "$@"

parser.c: parser.lemon base.c Makefile lemon
	./lemon -s -q "$<"
	cat base.c >> "$@"
	sed -i 's!^#line.*$$!/* & */!g' "$@"
	sed -i 's/YY/JJ/g; s/yy/jj/g; s/TOKEN/JTOKEN/g' "$@"

clean:
	-rm -f *.o *.lo

.PHONY: clean
