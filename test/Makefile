check: check-zombie check-newnet

check-zombie:
	newpid ./zombie.pl 2>&1 | tee zombie.out
	if grep -q 'version code' zombie.out; then sed -i -e '1,/version code/d' zombie.out; fi # remove "Non-standard uts for running kernel" on lucid
	diff -u zombie.expected zombie.out

check-newnet:
	( newpid -n ping -q -c 1 -n 127.0.0.1 | sed -e 's/\(time\|rtt\).*//'; \
	  newpid -n ping -q -c 1 -n 192.0.2.1 \
	) 2>&1 | tee newnet.out
	diff -u newnet.expected newnet.out

clean:
	rm -f zombie.out newnet.out
