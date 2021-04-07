+++
author = "Thomas Evensen"
date = "2021-03-10"
title =  "Code snippet for the ObservableReference"
tags = ["SwiftUI", "code snippets"]
categories = ["SwiftUI"]
description = "Why is the development of RsyncUI based on SwiftUI?"
lastmod = "2021-04-06"
+++
The [Swift code](https://github.com/rsyncOSX/RsyncUI/blob/main/RsyncUI/Model/Global/ObservableReferenceSSH.swift) for the StateObject:

```
import Combine
import Foundation

final class ObservableReferenceSSH: ObservableObject {
    // When property is changed set isDirty = true
    @Published var isDirty: Bool = false
    // Global SSH parameters
    // Have to convert String -> Int before saving
    // Set the current value as placeholder text
    @Published var sshport: String = ""
    // SSH keypath and identityfile, the settings View is picking up the current value
    // Set the current value as placeholder text
    @Published var sshkeypathandidentityfile: String = ""
    // If local public sshkeys are present
    @Published var localsshkeys: Bool = SshKeys().validatepublickeypresent()
    // Value to check if input field is changed by user
    @Published var inputchangedbyuser: Bool = false
    // Combine
    var subscriptions = Set<AnyCancellable>()

    init() {
        $inputchangedbyuser
            .sink { _ in
            }.store(in: &subscriptions)
        $sshkeypathandidentityfile
            .debounce(for: .seconds(2), scheduler: globalMainQueue)
            .sink { [unowned self] identityfile in
                sshkeypathandidentiyfile(identityfile)
            }.store(in: &subscriptions)
        $sshport
            .debounce(for: .seconds(2), scheduler: globalMainQueue)
            .sink { [unowned self] port in
                sshport(port)
            }.store(in: &subscriptions)
    }
}

extension ObservableReferenceSSH {
  // SSH identityfile
  private func checksshkeypathbeforesaving(_ keypath: String) throws -> Bool {
      ..
  }

  func sshkeypathandidentiyfile(_ keypath: String) {
      guard inputchangedbyuser == true else { return }
      // If keypath is empty set it to nil, e.g default value
      guard keypath.isEmpty == false else {
          SharedReference.shared.sshkeypathandidentityfile = nil
          isDirty = true
          return
      }
      do {
          let verified = try checksshkeypathbeforesaving(keypath)
          if verified {
              SharedReference.shared.sshkeypathandidentityfile = keypath
              isDirty = true
          }
      } catch let e {
          let error = e
          self.propogateerror(error: error)
      }
  }

  // SSH port number
  private func checksshport(_ port: String) throws -> Bool {
      ..
  }

  func sshport(_ port: String) {
      guard inputchangedbyuser == true else { return }
      // if port is empty set it to nil, e.g. default value
      guard port.isEmpty == false else {
          SharedReference.shared.sshport = nil
          isDirty = true
          return
      }
      do {
          let verified = try checksshport(port)
          if verified {
              SharedReference.shared.sshport = Int(port)
              isDirty = true
          }
      } catch let e {
          let error = e
          self.propogateerror(error: error)
      }
  }
}
```
