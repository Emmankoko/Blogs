### ALTQ INTEGRATION INTO NPF PACKET FILTER

Integrating Traffic shaping into NPF required that queues be defined in /etc/npf.conf configurations
 and particularly applied packets of a specific service.

Sayyy..

in etc/npf.conf

-----------------------------------------

$computer1_IP
$computer2_IP
$interface

altq on $interface cbq bandwidth 100Mb qlimit 60 priority 1 queues { mail, messages }
// define your child queues here
queue mail bandwidth 10% priority 0 cbq

group "external" on $interface {
    pass in on $interface from $computer1_IP to $computer2_IP queue mail// append your queue here
}

basicqlly the idea is to enqueue (altq_enqueue -> cbq_enqueue) packets passed on this rule which are given
altq tags so it doesn't join the normal IFENQUEUE(first in first out ) queueing on the network interface.

- Design
states of ALTQ must be tracked (stateful integration I call it).
ALTQ should be added, attached and enabled so our packets can be enqueued which is directly from /sys/altq/altq_subr.c codebase.

in doing this, all altq wrappers functions in NPF that calls the altq_add, altq_attach,
and altq_enable function must be in #ifdef ALTQ blocks and the opt_altq.h kernel option header must be included.

but the kernel options being enclosed in #_KERNEL_OPT blocks are resolved at build time. at load times of the modules, they are
not exposed to the kernel options so the kernel options blocks will remain uncompiled.

teasing myself right in the face. removing the kerel options to compile and i still get the functions from ALTQ innefective.
basically (enable, add, attach, etc).

the statically inbuilt version of npf works well with static version altq but the modular versions of npf doesn't work with altq since
we don't have a modular verion of ALTQ.

TODO:
Modularize ALTQ.

goals:
    implemented hooks to extend the functionality of npf to use functions from ALTQ.
    after thses hooks work well to compat modular npf with modular altq, we can finally reach the integrated npf and altq

