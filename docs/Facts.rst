Facts
======


Now let collect facts from a F5 and store those facts into a json file.

We will need to make a new entry into our inventory file:

::

    [adc]
    BigIp1 ansible_host=x.x.x.x


.. code-block:: yaml
   :linenos:


    ---
    - hosts: [adc]
      gather_facts: false
      connection: local

      tasks:

      - name: Gather F5 Info
        bigip_device_facts:
          provider:
          gather_subset:
            - system-info
            - interfaces
            - vlans
            - http-monitors
            - virtual-servers
            - partitions
            - self-ips
            - ltm-pools
            - nodes
        delegate_to: localhost
        register: bigip_fact_out

      - name: Copy facts to file
        copy:
          dest: facts.json
          content: "{{ bigip_fact_out }}"

.. centered::  f5.yml
