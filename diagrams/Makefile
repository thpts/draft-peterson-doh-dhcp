.PHONY: clean generate

venv: requirements.txt
	type virtualenv >/dev/null
	rm -rf venv
	(virtualenv venv --python=`which python3.6` && venv/bin/pip install --upgrade pip && venv/bin/pip install -r $<) || rm -rf venv

clean:
	rm -rf venv

generate:
	PYTHONPATH=src:${PYTHONPATH} protocol "Code:8,Len:8,URI Template:48" > dhcpv4.txt
	PYTHONPATH=src:${PYTHONPATH} protocol "option-code:16,option-len:16,URI Template:64" > dhcpv6.txt
	PYTHONPATH=src:${PYTHONPATH} protocol "Type:8,Len:8,URI Template:64" > ra.txt
