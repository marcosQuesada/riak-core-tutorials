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
	chmod 755 rel/mfmn/bin/mfmn

devrel: dev1 dev2 dev3

dev1 dev2 dev3:
	mkdir -p dev
	(cd rel && ../rebar generate target_dir=../dev/$@ overlay_vars=vars/$@.config)
	chmod 755 rel/mfmn/bin/mfmn

dev-start-nodes:
	for d in dev/dev* ; do \
		$$d/bin/mfmn start ; \
	done

dev-ping-nodes:
	for d in dev/dev* ; do \
		$$d/bin/mfmn ping ; \
	done

dev-join-nodes:
	for d in dev/dev* ; do \
		$$d/bin/mfmn-admin join mfmn1@127.0.0.1 ; \
	done

dev-ring-ready:
	./dev/dev1/bin/mfmn-admin ringready

dev-stop-nodes:
	for number in dev/dev* ; do \
		$$number/bin/mfmn stop ; \
	done

dev-attach-node:
	./dev/dev$(node)/bin/mfmn attach