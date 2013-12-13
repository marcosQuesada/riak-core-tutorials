.PHONY: deps

all: deps compile

compile:
	./rebar compile

deps:
	./rebar get-deps

clean:
	./rebar clean

distclean: clean devclean relclean
	./rebar delete-deps

rel: all
	./rebar generate
	chmod 755 rel/rts/bin/rts

relclean:
	rm -rf rel/rts

devrel: dev1 dev2 dev3

dev1 dev2 dev3:
	mkdir -p dev
	(cd rel && ../rebar generate target_dir=../dev/$@ overlay_vars=vars/$@.config)
	chmod 755 rel/rts/bin/rts

devclean:
	rm -rf dev

dev-start-nodes:
	for d in dev/dev* ; do \
		$$d/bin/rts start ; \
	done

dev-ping-nodes:
	for d in dev/dev* ; do \
		$$d/bin/rts ping ; \
	done

dev-join-nodes:
	for d in dev/dev* ; do \
		$$d/bin/rts-admin join rts1@127.0.0.1 ; \
	done

dev-ring-ready:
	./dev/dev1/bin/rts-admin ringready

dev-stop-nodes:
	for number in dev/dev* ; do \
		$$number/bin/rts stop ; \
	done

dev-attach-node:
	./dev/dev$(node)/bin/rts attach