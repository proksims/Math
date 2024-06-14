CC = gcc
FLAGS = -Wall -Werror -Wextra 

all: s21_math.a

s21_math.a: 
	$(CC) $(FLAGS) -c "s21_math.c" "s21_math.h"
	ar rc s21_math.a s21_math.o
	ranlib s21_math.a

test: clean s21_math.a
	$(CC) $(FLAGS) -lcheck s21_math.c s21_math_test.c -o s21_math_test
	./s21_math_test
	
gcov_report:
	$(CC) --coverage s21_math_test.c s21_math.c $(FLAGS) -lcheck -o test
	./test
	lcov -t "test" -o test.info -c -d .
	genhtml -o report test.info
	open report/index.html

clean:
	rm -rf *.o *.a *.g* 
	rm -rf s21_math s21_math_test
	rm -rf test.info test report

rebuild: clean all

style:
	clang-format -style=google -n ./s21_math.c
	clang-format -style=google -n ./s21_math.h
	clang-format -style=google -n ./s21_math_test.c
	python3 ./cpplint.py --extensions=c ./s21_math.c
