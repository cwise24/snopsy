Facts
======


Now let collect facts from a F5 and store those facts into a json file.

We will need to make a new entry into our inventory file:

.. code-block:: yaml 
   :caption: inventory group adc

    [adc]
    BigIp1 ansible_host=


.. code-block:: yaml
   :linenos:
   :caption: f5.yml 


    ---
    - hosts: [adc]
      gather_facts: false
      connection: local
    
      vars:
        provider:
           server: 
           user: "f5guest"
           password: ""
           validate_certs: no  

      tasks:

      - name: Gather F5 Info
        bigip_device_facts:
          provider: "{{ provider }}"
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
