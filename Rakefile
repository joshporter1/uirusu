# Copyright (c) 2012-2016 Arxopia LLC.
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
#     * Redistributions of source code must retain the above copyright
#       notice, this list of conditions and the following disclaimer.
#     * Redistributions in binary form must reproduce the above copyright
#       notice, this list of conditions and the following disclaimer in the
#       documentation and/or other materials provided with the distribution.
#     * Neither the name of the Arxopia LLC nor the names of its contributors
#     	may be used to endorse or promote products derived from this software
#     	without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
# WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL ARXOPIA LLC BE LIABLE FOR ANY DIRECT, INDIRECT,
# INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
# LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA,
# OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
# LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
# OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED
# OF THE POSSIBILITY OF SUCH DAMAGE.

$LOAD_PATH.unshift File.expand_path("../lib", __FILE__)

require "uirusu"
require 'rake'
require 'rake/testtask'

task :build do
	system "gem build #{Uirusu::APP_NAME}.gemspec"
end

task :tag_and_bag do
	system "git tag -a v#{Uirusu::VERSION} -m 'version #{Uirusu::VERSION}'"
	system "git push --tags"
	system "git checkout master"
	system "git merge dev"
	system "git push"
end

task :push => [:build] do
	system "gem push #{Uirusu::APP_NAME}-#{Uirusu::VERSION}.gem"
end

task :release => [:tag_and_bag, :push] do
	puts "Just released #{Uirusu::APP_NAME} v#{Uirusu::VERSION}. #{Uirusu::APP_NAME} is rubygem for using the Virustotal web service! More information at #{Uirusu::HOME_PAGE}"
end

task :clean do
	system "rm *.gem"
	system "rm -rf coverage"
end

task :default => [:test]

Rake::TestTask.new("test") do |t|
	t.libs << "test"
	t.pattern = 'test/*/*_test.rb'
	t.verbose = true
end
