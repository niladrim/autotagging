#!/bin/sh

if [ -f tags ]; then
	echo "delete tags file."
	rm tags
fi

if [ -f cscope.files ]; then
	echo "delete cscope.files file."
	rm cscope.files
fi

if [ -f cscope.out ]; then
	echo "delete cscope.out file."
	rm cscope.out
fi

echo "tags file is creating......."
ctags -R

echo "cscope.files file is creating......."
find $PWD \( -name '*.py' -o -name '*.c' -o -name '*.cpp' -o -name '*.cc' -o -name '*.h' -o -name '*.s' -o -name '*.S' -o -name '*.java' -o -name '*.dtsi' -o -name '*.dts' -o -name '*.cl' \) -print > cscope.files

echo "cscope.out file is creating......."
cscope -b -i cscope.files
