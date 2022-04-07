TMPDIR := tmp

# Find all .proto files.
PROTO_FILES := $(wildcard ../opentelemetry/proto/*/*/*.proto ../opentelemetry/proto/*/*/*/*.proto)

# Function to execute a command. Note the empty line before endef to make sure each command
# gets executed separately instead of concatenated with previous one.
# Accepts command to execute as first parameter.
define exec-command
$(1)

endef

doc:
	rm -rf ./$(TMPDIR)
	mkdir -p ./$(TMPDIR)
	$(foreach file,$(PROTO_FILES),$(call exec-command, sed 's/opentelemetry\/proto\/.*\/v1\///' $(file)> $(TMPDIR)/`basename $(file)` ))
	docker run --rm -v `pwd`:/out -v `pwd`/$(TMPDIR):/protos  pseudomuto/protoc-gen-doc
	rm -rf ./$(TMPDIR)
